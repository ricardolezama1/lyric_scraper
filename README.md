# -*- coding: utf-8 -*-
"""
Created on Sat Oct 16 22:36:11 2021

@author: Ricardo Lezama

https://ricardolezama.com

"""

import requests
 # importing the BeautifulSoup library in the program 
from bs4 import BeautifulSoup 
import sys

def lyrics_url(web_link):
    """
    This helps create a BS4 object. 
    
    Args: web_link containing references. 
    
    return: text with content. 
    """
    artist = requests.get(web_link).text
    check_soup = BeautifulSoup(artist, 'html.parser')
    return check_soup.find_all('div', class_='cnt-letra p402_premium')
    
   
##url = 'https://www.letras.com/conejo/'


def artist_songs_url(web_link):
    """
    This helps land into the URL's of the songs for an artist.'
    
    Args: web link is the 
    
    Return songs from https://www.letras.com/gru-;/
    """
    artist = requests.get(web_link).text
    print("Status Code", requests.get(web_link).status_code)
    check_soup = BeautifulSoup(artist, 'html.parser') 
    songs = check_soup.find_all('li', class_='cnt-list-row -song')
    return songs
#@ div class="cnt-letra p402_premium

def generate_text(url):
    import uuid 
    songs = artist_songs_url(url)
    for a in songs:
        song_lyrics = lyrics_url(a['data-shareurl'])
        print (a['data-shareurl'])
        new_file = open(str(uuid.uuid1()) +'results.txt', 'w', encoding='utf-8')
        new_file.write(str(song_lyrics[0]))
        new_file.close()
        print (song_lyrics)
    return print ('we have completed the download for ', url )


def main():
    artistas = open('artistas', 'r', encoding='utf-8').read().splitlines()
    url = 'https://www.letras.com/'
    for a in artistas : 
        generate_text(url + a +"/")
        print ('done')
#once complete, run copy *results output.txt to consolidate lyrics into a single page. 


if __name__ == '__main__':
    sys.exit(main())  # 




    
