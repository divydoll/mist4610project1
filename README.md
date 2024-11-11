# Group 9

JT Warren: https://github.com/JTwarren88/MIST4610gp1
Charlie Mixson: https://github.com/cjm75885/Project-1
Cassandra Albright: https://github.com/casalbright/MIST-4610-Project



# Data Model Forward Engineering
use ha_dsm67384;
CREATE TABLE teams ( team_id INT PRIMARY KEY, team_name VARCHAR(45), city VARCHAR(45), league VARCHAR(45), wins INT, draws INT, team_captain_id INT );

CREATE TABLE players ( player_id INT PRIMARY KEY, f_name VARCHAR(45), l_name VARCHAR(45), position VARCHAR(45), nationality VARCHAR(45), team_id INT, FOREIGN KEY (team_id) REFERENCES teams(team_id) );

CREATE TABLE playerStats ( player_id INT, goals INT, assists INT, passes INT, tackles INT, minutes_played INT, PRIMARY KEY (player_id), FOREIGN KEY (player_id) REFERENCES players(player_id) );

CREATE TABLE coaches ( coach_id INT PRIMARY KEY, cf_name VARCHAR(45), cl_name VARCHAR(45), start_date DATE, team_id INT, assistant_coach_id INT, FOREIGN KEY (team_id) REFERENCES teams(team_id), FOREIGN KEY (assistant_coach_id) REFERENCES coaches(coach_id) );

CREATE TABLE matches ( match_id INT PRIMARY KEY, match_date DATE, match_time TIME, match_loc VARCHAR(45) );

CREATE TABLE match_team_pairings ( team_id INT, match_id INT, PRIMARY KEY (team_id, match_id), FOREIGN KEY (team_id) REFERENCES teams(team_id), FOREIGN KEY (match_id) REFERENCES matches(match_id) );

CREATE TABLE matchStats ( team_id INT, match_id INT, shots_per_game INT, pass_percentage DECIMAL(5,2), fouls_per_game DECIMAL(4,2), goals_scored INT, result VARCHAR(45), PRIMARY KEY (team_id, match_id), FOREIGN KEY (team_id) REFERENCES teams(team_id), FOREIGN KEY (match_id) REFERENCES matches(match_id) );

ALTER TABLE teams ADD COLUMN team_captain_id INT;

ALTER TABLE teams ADD CONSTRAINT fk_team_captain FOREIGN KEY (team_captain_id) REFERENCES players(player_id);

-- Drop the foreign key constraint ALTER TABLE coaches DROP CONSTRAINT assistant_coach_id;

-- Drop the team_captain_id column ALTER TABLE teams DROP COLUMN team_captain_id;

-- Drop the foreign key constraint first ALTER TABLE coaches DROP FOREIGN KEY coaches_ibfk_2; -- This is an example name; use the actual foreign key constraint name if it's different

-- Drop the assistant_coach_id column ALTER TABLE coaches DROP COLUMN assistant_coach_id;

-- Add the assistant_coach_id column ALTER TABLE coaches ADD COLUMN assistant_coach_id INT;

-- Add the foreign key constraint ALTER TABLE coaches ADD CONSTRAINT fk_assistant_coach FOREIGN KEY (assistant_coach_id) REFERENCES coaches(coach_id);

INSERT INTO teams (team_id, team_name, city, league, wins, draws) VALUES (1, 'Manchester United', 'Manchester', 'EPL', 25, 10), (2, 'Real Madrid', 'Madrid', 'La Liga', 28, 7), (3, 'Bayern Munich', 'Munich', 'Bundesliga', 29, 6), (4, 'LA Galaxy', 'Los Angeles', 'MLS', 18, 12), (5, 'Liverpool', 'Liverpool', 'EPL', 23, 11), (6, 'Barcelona', 'Barcelona', 'La Liga', 27, 8), (7, 'Borussia Dortmund', 'Dortmund', 'Bundesliga', 26, 8), (8, 'New York City FC', 'New York', 'MLS', 17, 13), (9, 'Chelsea', 'London', 'EPL', 22, 12), (10, 'Atletico Madrid', 'Madrid', 'La Liga', 24, 9), (11, 'RB Leipzig', 'Leipzig', 'Bundesliga', 21, 10), (12, 'Seattle Sounders', 'Seattle', 'MLS', 16, 14), (13, 'Tottenham Hotspur', 'London', 'EPL', 21, 10), (14, 'Real Betis', 'Seville', 'La Liga', 19, 12), (15, 'Eintracht Frankfurt', 'Frankfurt', 'Bundesliga', 20, 11), (16, 'Inter Miami', 'Miami', 'MLS', 12, 16), (17, 'Arsenal', 'London', 'EPL', 24, 8), (18, 'Sevilla', 'Seville', 'La Liga', 20, 13), (19, 'VfB Stuttgart', 'Stuttgart', 'Bundesliga', 18, 15), (20, 'Chicago Fire', 'Chicago', 'MLS', 14, 14);

INSERT INTO players (player_id, f_name, l_name, position, nationality, team_id) VALUES (5, 'Bruno', 'Fernandes', 'Midfielder', 'Portuguese', 1), (10, 'Karim', 'Benzema', 'Forward', 'French', 2), (15, 'Joshua', 'Kimmich', 'Defender', 'German', 3), (20, 'Javier', 'Hernandez', 'Forward', 'Mexican', 4), (25, 'Mohamed', 'Salah', 'Forward', 'Egyptian', 5), (30, 'Lionel', 'Messi', 'Forward', 'Argentinian', 6), (35, 'Erling', 'Haaland', 'Forward', 'Norwegian', 7), (40, 'Maxi', 'Moralez', 'Midfielder', 'Argentinian', 8), (45, 'Mason', 'Mount', 'Midfielder', 'English', 9), (50, 'João', 'Felix', 'Forward', 'Portuguese', 10), (55, 'Christopher', 'Nkunku', 'Forward', 'French', 11), (60, 'Raúl', 'Ruidíaz', 'Forward', 'Peruvian', 12), (65, 'Harry', 'Kane', 'Forward', 'English', 13), (70, 'Nabil', 'Fekir', 'Midfielder', 'French', 14), (75, 'Filip', 'Kostić', 'Midfielder', 'Serbian', 15), (80, 'Gonzalo', 'Higuaín', 'Forward', 'Argentinian', 16), (85, 'Bukayo', 'Saka', 'Midfielder', 'English', 17), (90, 'Ivan', 'Rakitic', 'Midfielder', 'Croatian', 18), (95, 'Sasa', 'Kalajdzic', 'Forward', 'Austrian', 19), (100, 'Robert', 'Beric', 'Forward', 'Slovenian', 20), (105, 'Marcus', 'Rashford', 'Forward', 'English', 1), (110, 'Luka', 'Modric', 'Midfielder', 'Croatian', 2), (115, 'Leon', 'Goretzka', 'Midfielder', 'German', 3), (120, 'Jonathan', 'Dos Santos', 'Midfielder', 'Mexican', 4), (125, 'Sadio', 'Mané', 'Forward', 'Senegalese', 5), (130, 'Frenkie', 'de Jong', 'Midfielder', 'Dutch', 6), (135, 'Marco', 'Reus', 'Midfielder', 'German', 7), (140, 'Alexandru', 'Mitrita', 'Midfielder', 'Romanian', 8), (145, 'Christian', 'Pulisic', 'Midfielder', 'American', 9), (150, 'Saúl', 'Niguez', 'Midfielder', 'Spanish', 10), (155, 'Dani', 'Olmo', 'Midfielder', 'Spanish', 11), (160, 'Nicolás', 'Lodeiro', 'Midfielder', 'Uruguayan', 12), (165, 'Son', 'Heung-Min', 'Forward', 'South Korean', 13), (170, 'Sergio', 'Canales', 'Midfielder', 'Spanish', 14), (175, 'André', 'Silva', 'Forward', 'Portuguese', 15), (180, 'Blaise', 'Matuidi', 'Midfielder', 'French', 16), (185, 'Gabriel', 'Martinelli', 'Forward', 'Brazilian', 17), (190, 'Lucas', 'Ocampos', 'Forward', 'Argentinian', 18), (195, 'Silas', 'Katompa', 'Forward', 'Congolese', 19), (200, 'Ignacio', 'Aliseda', 'Forward', 'Argentinian', 20);

INSERT INTO playerStats (player_id, goals, assists, passes, tackles, minutes_played) VALUES (5, 10, 15, 1800, 50, 3000), (10, 25, 10, 1600, 25, 3100), (15, 4, 10, 2200, 80, 3050), (20, 12, 5, 1200, 20, 2750), (25, 22, 8, 1900, 30, 2900), (30, 30, 12, 2100, 20, 3200), (35, 40, 5, 1100, 10, 3400), (40, 5, 7, 1500, 35, 2900), (45, 7, 12, 2000, 25, 3050), (50, 8, 10, 1900, 20, 3100);

INSERT INTO coaches (coach_id, cf_name, cl_name, start_date, team_id) VALUES (1, 'Erik', 'ten Hag', '2022-06-01', 1), (2, 'Carlo', 'Ancelotti', '2021-07-01', 2), (3, 'Julian', 'Nagelsmann', '2020-07-01', 3), (4, 'Greg', 'Vanney', '2021-01-10', 4), (5, 'Jürgen', 'Klopp', '2015-10-08', 5), (6, 'Xavi', 'Hernández', '2021-11-06', 6), (7, 'Edin', 'Terzić', '2021-05-01', 7), (8, 'Ronny', 'Deila', '2020-03-01', 8), (9, 'Graham', 'Potter', '2022-09-08', 9), (10, 'Diego', 'Simeone', '2011-12-23', 10), (11, 'Marco', 'Rose', '2021-09-01', 11), (12, 'Brian', 'Schmetzer', '2016-07-26', 12), (13, 'Antonio', 'Conte', '2021-11-02', 13), (14, 'Manuel', 'Pellegrini', '2020-08-03', 14), (15, 'Oliver', 'Glasner', '2021-06-01', 15), (16, 'Tata', 'Martino', '2020-08-01', 16), (17, 'Mikel', 'Arteta', '2019-12-20', 17), (18, 'José', 'Luis Mendilibar', '2023-03-21', 18), (19, 'Sebastian', 'Hoeneß', '2023-04-03', 19), (20, 'Frank', 'Kloppas', '2023-04-02', 20);

INSERT INTO matches (match_id, match_date, match_time, match_loc) VALUES (1, '2024-01-15', '15:30:00', 'Old Trafford'), (2, '2024-01-18', '18:00:00', 'Santiago Bernabéu'), (3, '2024-01-20', '16:00:00', 'Allianz Arena'), (4, '2024-01-22', '14:00:00', 'Dignity Health Sports Park'), (5, '2024-01-25', '19:00:00', 'Anfield'), (6, '2024-01-28', '20:00:00', 'Camp Nou'), (7, '2024-01-30', '17:30:00', 'Signal Iduna Park'), (8, '2024-02-02', '16:45:00', 'Yankee Stadium'), (9, '2024-02-05', '14:30:00', 'Stamford Bridge'), (10, '2024-02-08', '19:15:00', 'Wanda Metropolitano'), (11, '2024-02-11', '16:00:00', 'Red Bull Arena'), (12, '2024-02-14', '18:30:00', 'Lumen Field'), (13, '2024-02-17', '15:45:00', 'Tottenham Hotspur Stadium'), (14, '2024-02-20', '13:30:00', 'Benito Villamarín Stadium'), (15, '2024-02-23', '20:30:00', 'Deutsche Bank Park'), (16, '2024-02-26', '21:00:00', 'DRV PNK Stadium'), (17, '2024-02-29', '17:15:00', 'Emirates Stadium'), (18, '2024-03-03', '18:00:00', 'Ramón Sánchez Pizjuán Stadium'), (19, '2024-03-06', '14:00:00', 'Mercedes-Benz Arena'), (20, '2024-03-09', '20:00:00', 'Soldier Field'), (21, '2024-03-12', '15:00:00', 'Old Trafford'), (22, '2024-03-15', '18:00:00', 'Santiago Bernabéu'), (23, '2024-03-18', '16:00:00', 'Allianz Arena'), (24, '2024-03-21', '14:00:00', 'Dignity Health Sports Park'), (25, '2024-03-25', '19:00:00', 'Anfield'), (26, '2024-03-28', '20:00:00', 'Camp Nou'), (27, '2024-03-30', '17:30:00', 'Signal Iduna Park'), (28, '2024-04-02', '16:45:00', 'Yankee Stadium'), (29, '2024-04-05', '14:30:00', 'Stamford Bridge'), (30, '2024-04-08', '19:15:00', 'Wanda Metropolitano'), (31, '2024-04-11', '16:00:00', 'Red Bull Arena'), (32, '2024-04-14', '18:30:00', 'Lumen Field'), (33, '2024-04-17', '15:45:00', 'Tottenham Hotspur Stadium'), (34, '2024-04-20', '13:30:00', 'Benito Villamarín Stadium'), (35, '2024-04-23', '20:30:00', 'Deutsche Bank Park'), (36, '2024-04-26', '21:00:00', 'DRV PNK Stadium'), (37, '2024-04-29', '17:15:00', 'Emirates Stadium'), (38, '2024-05-02', '18:00:00', 'Ramón Sánchez Pizjuán Stadium'), (39, '2024-05-05', '14:00:00', 'Mercedes-Benz Arena'), (40, '2024-05-08', '20:00:00', 'Soldier Field'), (41, '2024-05-11', '15:30:00', 'Old Trafford'), (42, '2024-05-14', '18:00:00', 'Santiago Bernabéu'), (43, '2024-05-17', '16:00:00', 'Allianz Arena'), (44, '2024-05-20', '14:00:00', 'Dignity Health Sports Park'), (45, '2024-05-25', '19:00:00', 'Anfield'), (46, '2024-05-28', '20:00:00', 'Camp Nou'), (47, '2024-06-01', '17:30:00', 'Signal Iduna Park'), (48, '2024-06-03', '16:45:00', 'Yankee Stadium'), (49, '2024-06-06', '14:30:00', 'Stamford Bridge'), (50, '2024-06-09', '19:15:00', 'Wanda Metropolitano');

INSERT INTO match_team_pairings (team_id, match_id) VALUES (1, 1), (2, 1), (3, 2), (4, 2), (5, 3), (6, 3), (7, 4), (8, 4), (9, 5), (10, 5), (11, 6), (12, 6), (13, 7), (14, 7), (15, 8), (16, 8), (17, 9), (18, 9), (19, 10), (20, 10), (1, 11), (3, 11), (5, 12), (7, 12), (9, 13), (11, 13), (13, 14), (15, 14), (17, 15), (19, 15), (2, 16), (4, 16), (6, 17), (8, 17), (10, 18), (12, 18), (14, 19), (16, 19), (18, 20), (20, 20), (1, 21), (2, 21), (3, 22), (4, 22), (5, 23), (6, 23), (7, 24), (8, 24), (9, 25), (10, 25), (11, 26), (12, 26), (13, 27), (14, 27), (15, 28), (16, 28), (17, 29), (18, 29), (19, 30), (20, 30), (1, 31), (3, 31), (5, 32), (7, 32), (9, 33), (11, 33), (13, 34), (15, 34), (17, 35), (19, 35), (2, 36), (4, 36), (6, 37), (8, 37), (10, 38), (12, 38), (14, 39), (16, 39), (18, 40), (20, 40);

INSERT INTO matchStats (team_id, match_id, shots_per_game, pass_percentage, fouls_per_game, goals_scored, result) VALUES -- Match 1: Manchester United vs Real Madrid (1, 1, 15, 85.3, 9, 2, 'Win'), (2, 1, 12, 82.7, 10, 1, 'Loss'),

-- Match 2: Bayern Munich vs LA Galaxy (3, 2, 18, 88.9, 7, 3, 'Win'), (4, 2, 10, 75.4, 11, 1, 'Loss'),

-- Match 3: Liverpool vs Barcelona (5, 3, 14, 83.5, 8, 2, 'Draw'), (6, 3, 14, 84.6, 9, 2, 'Draw'),

-- Match 4: Borussia Dortmund vs NYCFC (7, 4, 13, 80.1, 8, 1, 'Loss'), (8, 4, 16, 87.4, 3, 2, 'Win'),

-- Match 5: Chelsea vs Atletico Madrid (9, 5, 12, 81.2, 12, 1, 'Loss'), (10, 5, 17, 85.7, 2, 2, 'Win'),

-- Match 6: RB Leipzig vs Seattle Sounders (11, 6, 18, 89.8, 6, 3, 'Win'), (12, 6, 14, 81.4, 8, 1, 'Loss'),

-- Match 7: Tottenham Hotspur vs Real Betis (13, 7, 12, 82.5, 7, 1, 'Loss'), (14, 7, 17, 86.2, 2, 2, 'Win'),

-- Match 8: Eintracht Frankfurt vs Inter Miami (15, 8, 11, 79.4, 10, 0, 'Loss'), (16, 8, 14, 84.2, 8, 1, 'Win'),

-- Match 9: Arsenal vs Sevilla (17, 9, 15, 87.6, 6, 2, 'Win'), (18, 9, 11, 80.8, 9, 1, 'Loss'),

-- Match 10: VfB Stuttgart vs Chicago Fire (19, 10, 16, 88.5, 5, 3, 'Win'), (20, 10, 14, 83.2, 7, 1, 'Loss'),

-- Match 11: Manchester United vs Bayern Munich (1, 11, 13, 82.1, 10, 1, 'Loss'), (3, 11, 16, 87.5, 8, 3, 'Win'),

-- Match 12: Liverpool vs Borussia Dortmund (5, 12, 17, 86.3, 7, 3, 'Win'), (7, 12, 12, 79.9, 9, 1, 'Loss'),

-- Match 13: Chelsea vs RB Leipzig (9, 13, 14, 82.5, 8, 2, 'Draw'), (11, 13, 15, 83.6, 8, 2, 'Draw'),

-- Match 14: Tottenham Hotspur vs Eintracht Frankfurt (13, 14, 16, 88.1, 6, 2, 'Win'), (15, 14, 11, 78.4, 9, 1, 'Loss'),

-- Match 15: Arsenal vs Inter Miami (17, 15, 18, 85.5, 6, 3, 'Win'), (16, 15, 13, 80.7, 8, 1, 'Loss'),

-- Match 16: Real Madrid vs LA Galaxy (2, 16, 14, 85.8, 9, 2, 'Win'), (4, 16, 9, 76.5, 10, 1, 'Loss'),

-- Match 17: Barcelona vs NYCFC (6, 17, 17, 89.5, 5, 4, 'Win'), (8, 17, 13, 81.4, 7, 2, 'Loss'),

-- Match 18: Atletico Madrid vs Seattle Sounders (10, 18, 15, 83.6, 6, 3, 'Win'), (12, 18, 12, 79.1, 9, 1, 'Loss'),

-- Match 19: Sevilla vs Chicago Fire (18, 19, 11, 79.8, 11, 1, 'Loss'), (20, 19, 13, 84.9, 8, 2, 'Win'),

-- Match 20: VfB Stuttgart vs Real Betis (19, 20, 14, 86.4, 8, 2, 'Win'), (14, 20, 13, 81.7, 7, 1, 'Loss'),

-- Match 21: Manchester United vs Real Madrid (1, 21, 12, 81.2, 9, 1, 'Loss'), (2, 21, 16, 88.2, 7, 2, 'Win'),

-- Match 22: Bayern Munich vs LA Galaxy (3, 22, 18, 87.4, 8, 3, 'Win'), (4, 22, 11, 74.5, 9, 1, 'Loss'),

-- Match 23: Liverpool vs Barcelona (5, 23, 16, 85.6, 8, 2, 'Draw'), (6, 23, 14, 82.5, 8, 2, 'Draw'),

-- Match 24: Borussia Dortmund vs NYCFC (7, 24, 12, 78.6, 11, 1, 'Loss'), (8, 24, 15, 84.2, 7, 2, 'Win'),

-- Match 25: Chelsea vs Atletico Madrid (9, 25, 11, 79.3, 12, 1, 'Loss'), (10, 25, 14, 83.9, 6, 2, 'Win'),

-- Match 26: RB Leipzig vs Seattle Sounders (11, 26, 16, 86.5, 7, 3, 'Win'), (12, 26, 13, 80.2, 9, 1, 'Loss'),

-- Match 27: Tottenham Hotspur vs Real Betis (13, 27, 13, 81.7, 7, 1, 'Loss'), (14, 27, 17, 86.9, 5, 2, 'Win'),

-- Match 28: Eintracht Frankfurt vs Inter Miami (15, 28, 12, 79.4, 9, 0, 'Loss'), (16, 28, 15, 85.3, 6, 2, 'Win'),

-- Match 29: Arsenal vs Sevilla (17, 29, 18, 88.4, 6, 3, 'Win'), (18, 29, 11, 80.1, 8, 1, 'Loss'),

-- Match 30: VfB Stuttgart vs Chicago Fire (19, 30, 15, 86.7, 5, 3, 'Win'), (20, 30, 14, 82.8, 7, 1, 'Loss');

-- Update the assistant_coach_id with appropriate values UPDATE coaches SET assistant_coach_id = 1 WHERE coach_id = 3; UPDATE coaches SET assistant_coach_id = 2 WHERE coach_id = 4; UPDATE coaches SET assistant_coach_id = 1 WHERE coach_id = 5; UPDATE coaches SET assistant_coach_id = 7 WHERE coach_id = 6; UPDATE coaches SET assistant_coach_id = 8 WHERE coach_id = 7; UPDATE coaches SET assistant_coach_id = 7 WHERE coach_id = 8; UPDATE coaches SET assistant_coach_id = 2 WHERE coach_id = 9; UPDATE coaches SET assistant_coach_id = 2 WHERE coach_id = 10; UPDATE coaches SET assistant_coach_id = 9 WHERE coach_id = 11; UPDATE coaches SET assistant_coach_id = 15 WHERE coach_id = 12; UPDATE coaches SET assistant_coach_id = 12 WHERE coach_id = 13; UPDATE coaches SET assistant_coach_id = 12 WHERE coach_id = 14; UPDATE coaches SET assistant_coach_id = 7 WHERE coach_id = 15; UPDATE coaches SET assistant_coach_id = 15 WHERE coach_id = 16; UPDATE coaches SET assistant_coach_id = 15 WHERE coach_id = 17; UPDATE coaches SET assistant_coach_id = 6 WHERE coach_id = 18; UPDATE coaches SET assistant_coach_id = 2 WHERE coach_id = 19; UPDATE coaches SET assistant_coach_id = 1 WHERE coach_id = 20; UPDATE coaches SET assistant_coach_id = NULL WHERE coach_id = 1; UPDATE coaches SET assistant_coach_id = NULL WHERE coach_id = 2;

# Ten Queries

## 1. Identify the top 5 players with the most assists along with the teams they play for 

Identifying the top 5 players with the most assists and their respective teams is valuable for managers as it highlights key playmakers in the league, aiding in recruitment decisions, team strategy, and player valuations. Additionally, this data can be used for marketing purposes and to identify areas for player development, ultimately enhancing overall team performance and profitability.

select players.f_name, players.l_name, teams.team_name, playerStats.assists
from players join playerStats on players.player_id = playerStats.player_id join teams on teams.team_id = players.team_id order by playerStats.assists desc limit 5;


## 2. Identify the top scorers from each club 

Identifying the top scorers from each club helps managers understand which players are most effective at converting opportunities into goals, guiding decisions on player retention, recruitment, and tactical planning. It also provides insights for marketing and promotional efforts by highlighting standout performers to fans and potential sponsors.

select players.f_name, players.l_name, teams.team_name, playerStats.goals
from players join playerStats on players.player_id = playerStats.player_id join teams on teams.team_id = players.team_id WHERE playerStats.goals = ( SELECT MAX(playerStats.goals) FROM playerStats JOIN players ON playerStats.player_id = players.player_id WHERE teams.team_id = players.team_id) order by playerStats.goals desc;

## 3. Identify matches where a team scored more goals than their average and what were their results, shots pg and passes pg were 

Identifying matches where a team scored more goals than their average provides managers with insights into factors contributing to above-average performance, such as tactics, player form, or opponent weaknesses. Analyzing the results, shots per game, and passes per game in these matches can reveal patterns that help optimize strategies, improve training, and make data-driven decisions to replicate such high-scoring outcomes consistently.

SELECT matches.match_id, teams.team_name, matchStats.result, matchStats.shots_per_game, matchStats.pass_percentage FROM matches JOIN matchStats ON matches.match_id = matchStats.match_id JOIN teams ON teams.team_id = matchStats.team_id WHERE matchStats.goals_scored > ( SELECT AVG(matchStats.goals_scored) FROM matchStats WHERE teams.team_id = matchStats.team_id );

## 4. Provide a detailed breakdown of each player’s performance in different leagues, specifically focusing on their average goals scored per match and average pass percentage. 

By grouping the data by league and player, and then sorting by league and average goals scored, this query helps identify top performers in each league, making it valuable for comparing player efficiency and impact across different competitions. This information can assist managers, scouts, and analysts in evaluating player consistency and making data-driven decisions regarding player development, transfers, or strategic planning.

SELECT t.league, p.player_id, p.f_name, p.l_name, AVG(ms.goals_scored) AS avg_goals_per_match, AVG(ms.pass_percentage) AS avg_pass_percentage FROM players p JOIN teams t ON p.team_id = t.team_id JOIN playerStats ps ON p.player_id = ps.player_id JOIN match_team_pairings mtp ON t.team_id = mtp.team_id JOIN matchStats ms ON mtp.match_id = ms.match_id GROUP BY t.league, p.player_id, p.f_name, p.l_name ORDER BY t.league, avg_goals_per_match DESC;

## 5. Retrieve the players with the highest number of tackles from each team, along with their first name, last name, and team name. 

It allows managers and analysts to identify the best defensive players within each team, which is valuable for understanding defensive strengths, player contributions, and for making decisions about player training, positioning, and strategy. By sorting the results by team name, the query provides an organized view of top tacklers across all teams.

select f_name, l_name, team_name, tackles from players join playerStats on players.player_id = playerStats.player_id join teams on players.team_id = teams.team_id where tackles =( select max(tackles) from players as player_sub join playerStats on player_sub.player_id = playerStats.player_id where players.team_id = player_sub.team_id ) Order by team_name;

## 6. Retrieve detailed information about the player Lionel Messi, including his first name, last name, team name, and position. 

It helps quickly identify specific details about a well-known player and can be used for player profile generation, reporting, or verifying his current team and position, which can be useful for managers, fans, or analysts looking for up-to-date player information.

SELECT players.f_name, players.l_name, teams.team_name, players.position FROM players JOIN teams ON players.team_id = teams.team_id WHERE players.f_name = 'Lionel' AND players.l_name = 'Messi';

## 7. Calculate the total number of goals scored by Lionel Messi. 

It aggregates his goal count across all matches in the playerStats table, providing an overview of his scoring performance. This information can be used for player performance analysis, historical records, or comparisons against other players. It's valuable for managers, analysts, and fans who want to quantify Messi’s goal-scoring achievements.

SELECT SUM(playerStats.goals) FROM playerStats JOIN players ON playerStats.player_id = players.player_id WHERE players.f_name = 'Lionel' AND players.l_name = 'Messi';

## 8. Provide an overview of player performance based on nationality, showing the number of players and the total number of goals scored by players from each nationality.

It offers insights into how different nationalities contribute to overall performance. This information can help managers, analysts, and scouts identify strong talent pools by nationality, understand scoring patterns, and inform recruitment or scouting strategies.

select nationality, COUNT(f_name) AS num_players, SUM(goals) AS num_goals from players join playerStats on players.player_id = playerStats.player_id GROUP BY nationality;

## 9. Compare the performance of mentor-mentee coaching pairs based on the number of team wins

This analysis can provide insights into the effectiveness of mentorship programs, track mentee development, and highlight successful coaches who have outperformed their mentors.

select mentee.cf_name, mentee.cl_name, mentee_team.wins, mentor.cf_name, mentor.cl_name, mentor_team.wins from coaches as mentee join coaches as mentor on mentee.coach_id = mentor.assistant_coach_id join teams as mentee_team on mentee.team_id = mentee_team.team_id join teams as mentor_team on mentor.team_id = mentor_team.team_id where mentee_team.wins > mentor_team.wins;

## 10. Retrieve the teams and the corresponding match ID for teams that competed against each other at Old Trafford on January 15, 2024, at 3:30 PM. 

Retrieving this information is useful for managers, analysts, and fans to review specific matches played at a particular venue and time, such as Old Trafford. It helps identify key games, analyze performance metrics, and understand the context of team matchups. This data can also be used for scheduling, historical analysis, and preparing for future encounters between these teams at similar venues or conditions.

SELECT team_name, match_team_pairings.match_id FROM teams JOIN match_team_pairings ON teams.team_id = match_team_pairings.team_id JOIN matches ON matches.match_id = match_team_pairings.match_id WHERE matches.match_date = '2024-01-15' AND matches.match_time = '15:30:00' AND matches.match_loc = 'Old Trafford';

