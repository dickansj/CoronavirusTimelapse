This is a timelapse of the [New York Times U.S.A. Coronavirus map](https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html), built using the [Wayback Machine](https://web.archive.org/web/*/https://www.nytimes.com/interactive/2020/us/coronavirus-us-cases.html), along with the newly published [NYTimes database](https://github.com/nytimes/covid-19-data) for data before March 3.

I grabbed 4 snapshots per day from the Wayback Machine. The map on the website has changed its display parameters several times, so I took the current version as a template and scraped the html from old snapshots. The map keeps shrinking the scale of its circles as they grow, so I've normalized all the old data to match the current scale.

processHistory.py reads history.csv (which was built from NYTimes data) to create files which are then read, along with the original html dumps, by processHtml.py, which creates normalized html files. I then loaded each file into a browser in full screen and screenshotted the page, creating image files, which I batch cropped with [IrfanView](https://www.irfanview.com/) and then assembled into a video with the following [ffmpeg](https://www.ffmpeg.org/download.html) command: `ffmpeg/bin/ffmpeg.exe -f image2 -r 8 -i images/frame%03d.png -r 8 -c:a copy -c:v libx264 -crf 12 -preset veryslow CoronavirusTimelapse.mp4`
