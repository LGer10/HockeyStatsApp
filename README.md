# nhl-players

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```
# Documentation

## Projectidea
- Display statisticts about NHL-players in a list 
- GET detailed statistics about a specific player
- Display list with favourite players
- CREATE, READ, UPDATE, DELETE players

## Framework
- Vue.js
    -   BootstrapVue CSS
    -   Bootstrap CSS
    -   CSS

## Work Journal
- 26.03.2021: 
    - Described Projet idea and created mockups 
- KW 17: 
    - Created app layout and crud operations GET, CREATE and DELETE
- KW 18: 
    - Implemented crud operations UPDATE and include sportsdata.io API into app to fetch players data
        -   Tables used: 
            - PlayerSeasonStats
            - PlayerSeasonStatsByPlayer
    - improved layout and tried to better split up the project in components 


## Difficulties
-   Splitting up the project in components
    -   Data handling between componets
-   Including the sportsdata.io API 
    -   Visualizing these data in a list and filter it by name
    -   getting specific data from a player by id
-   Implementing the CRUD operation Update
    -   Problems with datatype mapping from restdb.io (int) DB and sportsdata.io (strangely the stats goals and assist are from datatype float) API
        
-   Layout und Style
    -   Trouble by using different styling frameworks 
        -   CSS
        -   Bootstrap CSS
        -   BootstrapVue

## Conclusion
### Positive
-   Learnd basics about Vue.js framework
-   Had quit fun doing a project in sports and i would like to take the project further and implement some visualizing of statistics
-   

### Lessons Learnd
-   Structure the project well from beginning
    -   I did lots of try and error what is fine but i lost quite the overview i.e where i used Bootstrap CSS and where BootstrapVue or just inline CSS. Also i had trouble with splitting up the project in different components. Specialy with handling data between components. So i implemented the most things directly in the app.vue file which worked well but is not well structured in components what Vue.js is designed for.
-   Maybe don't mix up too much the styling frameworks 
    -   Maybe that is totally normal, i don't know ;) but i had some problem with improving layout of the site in the end of the project. I. e, I implemented a table with BootsrapVue and one with normal CSS styling. I would probably try to have better focues on which ist the best framework for what thing i would like to implement and not just try one and look if it works.

-   Don't loose too much time for little details
    -   i kinda like to look at little details and invest some time in them but beside my thesis there was not much time left to do that. So sometimes i think  lost a bit too much time with things that were not key funcionalities in this project


```
Overall it was a fun project and i learned a lot about vue.js and JS :)