# S<sup>2</sup> Doubles Dataset
## Introduction
In this study, a technical data collection solution is proposed for the tactical analysis of badminton doubles match. The S<sup>2</sup>-Labeling was proposed and developed in literature, that enables mass competition data collection for badminton singles possible and affordable. An intuitive labeling tool is designed and implemented, which uses broadcast videos of badminton games as the data source. In this work, considering the property difference between singles game and doubles game, we define microscopic data for badminton doubles based on S<sup>2</sup>-
Labeling. Technical information of each shot in the match including hitting time, players' position, hitting posture, shuttlecock projected location, type of stroke, and the dead bird reason with faulting player. Moreover, a new labeling tool for recording shot-by-shot technical data of badminton doubles game is developed with computer vision techniques. Since the data of doubles is more complex than the singles one, algorithms are designed and implemented in the labeling tool to ensure a smooth and accurate labeling process. Furthermore, a prototype data representation is formulated and the court division definition used for pattern analysis is modified as well. In conclusion, the badminton doubles data collection tool, along with a series of graphics for information visualization, could assist players and coaches in reviewing the games within a day without the need for on-site professional sports performance analysts or high-priced photography equipment. An S<sup>2</sup> Doubles Labeling dataset composed of six badminton sets is shared with the community to facilitate further research. The dataset is publicly available at: https://github.com/HuangYuHsien/S2DoublesDataset.
## Dataset Structure
    S2 Doubles Data
    │  README.md - Record file information
    │  Match.csv - Record the basic information of each game
    │  doubles_court.png - The badminton court figure
    ├─Match 001 - Data folder for each game
    │  │  RallySeg.csv - Record rally frame tag and scoring
    │  ├─label - Data folder for shot-by-shot labeling data
    │  │  │   set1.csv
    │  │  │   set2.csv
    │  │  └─  set3.csv
    │  └─tracknet – Data folder for shuttle’s trajectory prediction of corresponding rally
    │     │   1_00_01.csv
    │     │   .
    │     │   .
    │     └─  3_21_12.csv     
    ├─Match 002
    │  .    
    │  .  
    └─Match 003
## Match Information
The videos could be fetched from BWF YouTube channel. The FPS of video should be 30 FPS.
- Match 001: DAIHATSU Indonesia Masters 2022, Men's Doubles, Finals, Alfian/Ardianto (INA) vs. Liang/Wang (CHN)
- Match 002: DAIHATSU Indonesia Masters 2022, Men's Doubles, Semifinals, Liang/Wang (CHN) vs. Gideon/Sukamuljo (INA)
- Match 003: DAIHATSU Indonesia Masters 2022, Mixed Doubles, Finals, Zheng/Huang (CHN) vs. Gicquel/Delrue (FRA)
## Match.csv
- `name`: match named after players' last name, tournament name, and round
- `tournament`: Tournament name
- `event`: doubles type (men's doubles, women's doubles, mixed doubles)
- `round`: round in the tournament (ex: finals, semi-finals)
- `year`, month, day: the date
- `set`: total set count
- `duration`: match duration (minute)
- `win_A`: the first player's name of the win team
- `win_B`: the second player's name of the win team
- `lose_C`: the first player's name of the lose team
- `lose_D`: the second player's name of the lose team
- `downcourt`: the team at the downcourt in the first set (0: win, 1: lose)
- `homography_matrix`: the homography matrix to map the point from video to `doubles_court.png`, which the corner points on the figure are (27, 100), (339, 100), (339, 784), (27, 784)
- The pixel coordinates (x, y) of the four court corners (up left, up right, down right, down left) on video
    - `upleft_x`
    - `upright_x`
    - `downright_x`
    - `downleft_x`
    - `upleft_y`
    - `upright_y`
    - `downright_y`
    - `downleft_y`
## RallySeg.csv
- `Score`: rally named after set number, win team score after this rally, lose team score after this rally
- `UpCourt`: players at upper-half court
- `DownCourt`: players at down-half court
- `Start`: start frame of the rally
- `End`: end frame of the rally
- `Comment`: if the video has problems to labels (0: no, 1: yes)
## label csv
- `rally`: rally number in the set
- `ball_round`: ball round number in the rally
- `time`: shot start time (hh:mm:ss)
- `start_frame`: shot start time (frame)
- `end_frame`: shot end time (frame)
- `roundscore_AB`: win team score after this rally
- `roundscore_CD`: lose team score after this rally
- `player`: player hit the shot (A, B, C, D)
- `server`: shot hitting type (1: serve, 2: return, 3:deadball)
- `ball_type`: ball type of the shot
- `backhand`: shot is hit in forehand or backhand (0: forehand, 1: backhand)
- `hit_height`: hitting height (1: over net, 2: below net)
- hitting point projection on the court, denoted by pixel coordinates (x, y) on video
    - `hit_x`
    - `hit_y`
- `return_height`: returning/landing height (1: over net, 2: below net)
- returning/landing point projection on the court, denoted by pixel coordinates (x, y) on video
    - `return_x`
    - `return_y`
- players' location (the center point of the player’s feet) projection on the court, denoted by pixel coordinates (x, y) on video
    - `player_A_x`
    - `player_A_y`
    - `player_B_x`
    - `player_B_y`
    - `player_C_x`
    - `player_C_y`
    - `player_D_x`
    - `player_D_y`
- `lose_reason`: reason for losing the rally
- `fault_player`: the playing who takes the responsibility for losing the rally
- `score_reason`: reason for winning the rally
- `score_team`: the team winning this rally (AB, CD)
- `flaw`: if the shot has flaws to label (0: no, 1: yes)
## tracknet csv
- `index`: frame number in the rally
- the shuttle position on video denoted by pixel coordinates (x, y)
	- `x`
	- `y`