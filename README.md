# Personal-Spotify-Dashboard

# INTRODUCTION
Every day, users generate large volumes of data simply by listening to music on streaming platforms. Platforms like Spotify capture detailed information about what users listen to, when they listen, and how their preferences evolve over time. This data has the potential to provide valuable insights into personal listening behaviour, favourite artists, and music consumption trends.

However, Spotify does not provide a fully interactive interface that allows users to explore their complete listening history in depth or visualize their listening patterns in a comprehensive and customizable way. As a result, users have limited ability to analyze their habits, identify trends, or gain deeper insights from their own data.

To address this gap, this project integrates data extraction using the Spotify API, extended streaming history exports, data enrichment, and interactive dashboard visualization. The goal is to create a complete, structured, and visual representation of user's music consumption, enabling deeper analysis and a better understanding of one's listening patterns over time.


# TABLE OF CONTENT

1. Introduction
2. Objective
3. Goals
4. Other Skills Demonstrated
5. Data Overview
6. Data Transformation
7. Data Modelling
8. Analysis
9. Recommendations
10. Conclusion

---

# OBJECTIVE

The primary objective of this project is to design and develop a comprehensive, interactive personal analytics dashboard that provides deep insights into user's music listening behaviour using their personal data from Spotify.

This project aims to go beyond the limitations of Spotify’s native interface by extracting, enriching, and transforming raw listening data into a structured format suitable for advanced analysis and visualization.

The project aims to:

- Extracts personal listening data from Spotify
- Overcomes Spotify API limitations by incorporating extended streaming history
- Enriches data with album covers, artist images, and Spotify links
- Transforms and structures the data for dashboard reporting
- Provides meaningful insights into listening behaviour
- Create a scalable data pipeline that can be refreshed and reused

---

# GOALS

The project is guided by the following technical, analytical, and visualization goals:

Data Engineering Goals

- Automate the extraction of personal Spotify data using Python
- Integrate multiple data sources into a unified dataset
- Clean, standardize, and prepare the data for analysis
- Enrich records with additional metadata and media assets
- Create reusable datasets for reporting and visualization

Data Analysis Goals

- Identify most frequently played tracks, artists, and albums
- Analyze listening trends over time (daily, monthly, yearly)
- Understand peak listening periods and behavioural patterns
- Track evolution of music taste over time

Visualization Goals

- Build a fully interactive dashboard to enable intuitive exploration of listening history
- Use track covers, album covers and artist images for visual storytelling
- Implement drill-down and navigation features
- Integrate direct links to open content in Spotify

---

# OTHER SKILLS DEMONSTRATED

**1. Analytical Thinking**

This project demonstrates my ability to convert raw data into meaningful insights.

Key analytical capabilities:
- Identifying trends and patterns
- Behavioural analysis
- Ranking and performance analysis
- Time-based analysis

**2. Problem Solving**

Several real-world challenges were solved during this project, including:

- Overcoming Spotify API limitations
- Integrating multiple data sources
- Handling incomplete or missing metadata
- Automating image downloads and processing

This demonstrates practical problem-solving ability in real data environments.

**3. End-to-End Project Development**

This project demonstrates full ownership of the data lifecycle:

Data Collection → Data Engineering → Data Modelling → Analysis → Visualization

This is the exact workflow used in professional data analyst and business intelligence roles.

---

# DATA OVERVIEW

The project uses two primary data sources:


**1. Spotify API Data**

Extracted using Python and Spotipy.

Includes:

**Recently Played**

Fields:
- Track Name
- Artist
- Album
- Played At
- Track ID
- Album Cover
- Artist Image
- Spotify Links


**Saved Tracks**

Includes all liked songs.


**Playlists**

Fields:
- Playlist name
- Tracks
- Artists
- Albums

**Top Tracks and Artists**

Across:
- Short term
- Medium term
- Long term


## Limitation of Spotify API

**Spotify API only provides the Last 50 recently played tracks**

This limitation prevents full historical analysis.


## 2. Extended Streaming History

To overcome this limitation, I requested my extended listening history from Spotify. https://www.spotify.com/us/account/privacy/download/

| Column                            | Description                                          |
| --------------------------------- | ---------------------------------------------------- |
| Ts                                | Timestamp when the track was played                  |
| Platform                          | Device or platform used (e.g., mobile, web, desktop) |
| Ms Played                         | Duration the track was played (in milliseconds)      |
| Conn Country                      | Country where the track was played                   |
| Ip Addr                           | IP address of the device                             |
| Master Metadata Track Name        | Name of the track                                    |
| Master Metadata Album Artist Name | Name of the artist                                   |
| Master Metadata Album Album Name  | Name of the album                                    |
| Spotify Track Uri                 | Unique Spotify identifier for the track              |
| Episode Name                      | Podcast episode name (if applicable)                 |
| Episode Show Name                 | Podcast show name                                    |
| Spotify Episode Uri               | Podcast episode URI                                  |
| Audiobook Title                   | Audiobook title (if applicable)                      |
| Audiobook Uri                     | Audiobook identifier                                 |
| Audiobook Chapter Uri             | Audiobook chapter identifier                         |
| Audiobook Chapter Title           | Audiobook chapter title                              |
| Reason Start                      | How playback started (e.g., click, autoplay)         |
| Reason End                        | How playback ended (e.g., track finished, skipped)   |
| Shuffle                           | Indicates if shuffle mode was used                   |
| Skipped                           | Indicates if the track was skipped                   |
| Offline                           | Indicates if played offline                          |
| Offline Timestamp                 | Timestamp when offline playback occurred             |
| Incognito Mode                    | Indicates if private session was enabled             |

Audiobook fields were excluded as they were not relevant to the analysis.

This enabled complete historical analysis from first listen till requested date


## 3. Enriched Metadata

Additional enrichment was performed using Spotify search API to retrieve:

- Spotify links
- Artist images
- Album covers
- Track covers

Images were downloaded and resized for dashboard integration.

---

# DATA TRANSFORMATION

Data transformation involved multiple steps:

## Step 1: Data Extraction

Spotify API was used to extract:

- Recently played
- Saved tracks
- Playlists
- Top tracks
- Top artists

Exported to Excel workbook as sheets.


## Step 2: Extended History Integration

Streaming history CSV was processed.

Columns were identified and extracted:

- Track name
- Album name
- Artist name


## Step 3: Data Enrichment
The extended streaming history dataset was enriched to include Spotify links and image URLs for tracks, albums, and artists using the Spotify Search API from Spotify.

To improve efficiency and reduce unnecessary API calls, the Python script first removed duplicate track, album, and artist names, ensuring that each unique item was searched only once.

For each unique item:
- The Spotify Search API was used to find the correct match
- The corresponding Spotify URL was retrieved to enable direct navigation
- The album cover image URL was retrieved for tracks and albums
- The artist image URL was retrieved for artists

The enriched results were then stored in separate structured tables(Sheets) and exported for further processing.


## Step 4: Image Download

To support image-based visualization in the dashboard, album covers, artist images, and track images were automatically downloaded and stored locally using Python.

The script automated the process by:
- Downloading images directly from the enriched image URLs obtained via the Spotify API
- Naming each image using the corresponding track, album, or artist name
- Removing invalid filename characters to ensure compatibility

To optimize the images for dashboard performance and consistency, each image was:
- Resized to 640 × 640 pixels
- Converted to JPG format
- Saved with high quality and optimized file size
- Stored in the Tableau Shapes folder for dashboard integration

This automation eliminated the need for manual downloads and ensured that all images were properly formatted and ready for use, enabling rich, image-driven visualizations within the dashboard.

---

# DATA MODELLING

Data was structured into logical tables:


## Fact Table:

**Extended Streaming History**

Contains:
- Track
- Artist
- Album
- Timestamp

This table drives listening analysis.


## Dimension Tables:

**Tracks**

Contains:

- Track metadata
- Cover image
- Spotify link

**Artists**

Contains:
- Artist name
- Artist image
- Spotify link


**Albums**

Contains:

- Album name
- Album image
- Spotify link


<img width="411" height="218" alt="image" src="https://github.com/user-attachments/assets/4b23c056-733c-4e65-9bec-2142a19d7bd1" />

"Button" dateset was used to data scaffolding where necessary

This created a star schema model suitable for dashboard reporting.

---

# ANALYSIS

The dashboard provides deep insights into personal listening behaviour across two main pages: **History** and **Patterns**.

## History Page

The History page focuses on individual listening activity and trends:

### Key Metrics and Trends
- Displays KPIs and line charts for:
    - Listening Time
    - Tracks Played
    - Artists Played
    - Albums Played
- Date range selector allows users to analyze different periods.
  Users can click the Date Range to access a slider or preset periods (e.g., last week, last month).

### Ranking and Tabs
- Tracks, Albums, and Artists are ranked by total listening time.
- Recently Played tracks are ranked by recency.
- All metrics can be accessed via separate tabs.

### Interactive Windows

Clicking on a Track, Album, or Artist cover opens a detailed drilldown window with:
 - Ranking (listening frequency)
 - Total listening time
 - Number of plays
 - Number of tracks and albums
 - Music types (genres)

### Spotify Integration
-  From the window, clicking the cover or name opens the item directly in Spotify.
- Top Tracks or Top Albums that displays on the window can also be clicked to play content immediately in Spotify.



## Pattern Page

The Pattern page analyzes listening habits and user persona:

### User Persona Classification
Each user is categorized into one of eight types:
- Active Skipper
- Replay Enthusiast
- Indecisive Clicker
- Intentional Selector
- Power Skipper
- Algorithm is my DJ
- Auto Skipper
- Passive Listener

### Heatmap Visualization
- Displays listening intensity by hour, day, and month.

### Preferences and Behaviour Tabs
- Platform, Offline, Podcast, and Skip Rate tabs.
- Bar charts show listening distribution across countries and shuffle usage.


This setup allows users to **explore their habits**, understand **listening patterns**, and make **data-driven decisions about their music experience**.

---


# RECOMMENDATIONS

This dashboard demonstrates how personal Spotify data can be transformed into an engaging and interactive experience for users. By exploring trends, rankings, and listening habits, users can uncover hidden patterns in their music taste, relive favourite moments, and gain meaningful insights into their listening behaviour. 

My key recommendation is: 
### SPOTIFY SHOULD CONSIDER COLLABORATING WITH ME TO DEPLOY THIS TOOL

Currently, the Spotify API limits data retrieval to the most recent 50 tracks, which restricts full automation. 

By collaborating, we could:
- **Integrate real-time Spotify data** or automate data refresh using scheduled scripts  
- **Deploy the dashboard online**, making it accessible to all users  
- **Add genre classification analysis** to provide deeper insights into musical preferences  
- **Analyze listening duration** to better understand engagement patterns  
- **Strengthen predictive models** for personalized song recommendations  

Implementing these enhancements would turn this project into a fully automated, interactive, and scalable tool for both Spotify and its users.


---

# CONCLUSION

This project transforms raw Spotify listening history into a dynamic, interactive, and visually rich dashboard that turns data into an experience. Users can explore their favourite tracks, albums, and artists, uncover hidden patterns in their music taste, and gain actionable insights into their listening behaviour over time.  

With further integration into Spotify’s ecosystem such as real-time updates, automated data refresh, genre and listening duration analysis, and enhanced recommendations, this tool could redefine how users interact with their music, making their listening journey more personal, playful, and insightful.  

Beyond providing personal insights, the project demonstrates end-to-end data expertise: extracting and enriching data, overcoming API limitations, structuring it for analysis, and delivering it through an interactive visualization. The process highlights how data can be both meaningful and engaging, bridging technical rigor with user experience.  

Ultimately, this dashboard is not just a collection of statistics; it’s a story of music, habits, and personal taste, giving users a deeper connection to the songs they love.

---
