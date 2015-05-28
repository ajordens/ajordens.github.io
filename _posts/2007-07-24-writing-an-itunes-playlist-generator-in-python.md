---
title: Writing an iTunes playlist generator in Python
author: ajordens
layout: post
permalink: /2007/07/writing-an-itunes-playlist-generator-in-python/
categories:
  - General Discussions
---
The following is some quick & dirty code on how one might approach the idea of writing a playlist generator in Python. 

The language almost doesn&#8217;t matter but ActivePython does ship with bindings that allow you easily interact with any Windows COM object. It worked nicely in conjunction with iTunes Windows SDK.

In the end it&#8217;s fairly trivial code hacked together in not much more than an hour or so but I&#8217;ve been quite happy with the playlists it creates.

**Basic Design:**

1) Provide a means for the caller to specify basic criteria for playlist generation. ie) # of songs, list of genre&#8217;s, propotion of songs per genre, etc. 

2) Retrieve a list of songs on an iPod and their metadata relevant to generation (name, genre, play count, etc.).

3) Implement a simple algorithm to choose the appropriate # of songs from each genre as per the original criteria.

4) Create the playlist in iTunes

**Code:** *(this was actually part of my last hack day project, so excuse the python inadequacies)*

<pre>#!/usr/bin/env python

import pythoncom, win32com.client, time
import sys, os
import csv
from random import Random, shuffle

SOURCE_ID = "Adam's iPod"
EXPORT_FILE = "ipod.data"
CRITERIA = {"name":"Test Playlist", 
            "count":25, 
            "genres":{"Alternative":.15, "Other":.25, "Rock":.60}, 
             "minPlayCount":5}

def main():
    print 'attaching to iTunes...'
    iTunes = win32com.client.gencache.EnsureDispatch("iTunes.Application")
    
    print 'connecting to ' + SOURCE_ID + '...'
    source = iTunes.Sources.ItemByName(SOURCE_ID)
    
    iPodTracks = source.Playlists.ItemByName("Music").Tracks
    libraryTracks = iTunes.LibraryPlaylist.Tracks
    
    name = CRITERIA["name"]
    count = CRITERIA["count"]
    minPlayCount = CRITERIA["minPlayCount"]
    genres = CRITERIA["genres"]

    print 'creating a playlist called "' + name + '" with ' + str(count) + ' songs'
    
    # Create a map of genre -> song where each song satisfies the minPlayCount criteria
    songsByGenre = {}
    for i in range(1, libraryTracks.Count):
        track = libraryTracks.Item(i)        
        if track.Genre in genres and track.PlayedCount > minPlayCount:
            tracks = songsByGenre.get(track.Genre, [])
            tracks.append(track)
            songsByGenre[track.Genre] = tracks

    # For each applicable genre, pull a quasi random set of tracks
    shuffle = Random(None).shuffle
    playlistTracks = []
    for genre in songsByGenre.keys():
        numSongs = int(round(genres[genre] * count))
        tracks = songsByGenre[genre]
        shuffle(tracks)
        print genre + ': ' + str(len(tracks[0:numSongs])) + ' songs'
        for track in tracks[0:numSongs]:
            playlistTracks.append(track)
            
    # Remove any pre-existing playlists that exist with the same name
    librarySource = iTunes.Sources.ItemByName("Library")
    for i in range(1, librarySource.Playlists.Count + 1):
        try:
            playlist = librarySource.Playlists.Item(i)
            playlist = win32com.client.CastTo(playlist, 'IITLibraryPlaylist')
            if playlist.Name == name:
                playlist.Delete()
        except:
            pass
        
    # Create the playlist and add the tracks.
    playlist = win32com.client.CastTo(iTunes.CreatePlaylist(name), 'IITLibraryPlaylist')    
    for track in playlistTracks:        
        playlist.AddTrack(track)
    
if __name__ == '__main__':
    main()
</pre>