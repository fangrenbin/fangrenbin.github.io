---
author: fangrenbin
comments: false
date: 2015-07-27 08:44:11+00:00
layout: post
slug: angularjs-tutorial
title: Angularjs Tutorial
wordpress_id: 655
categories:
- wordpress
---

##### Install npm(nodejs package management).



    
    
    apt-get install nodejs-legacy
    nodejs --version
    





##### Install tools


Bower - client-side code package manager
Http-Server - simple local static web server
Karma - unit test runner
Protractor - end to end (E2E) test runner

    
    
    npm install tool name
    





##### npm runs scripts



    
    
    npm start //start a local development web-server
    npm test //start the Karma unit test runner
    npm run protractor //run the Protractor end to end (E2E) tests
    npm run update-webdriver //install the drivers needed by Protractor
    





##### Search



    
    
    <div class="container-fluid">
        <div class="row">
          <div class="col-md-2">
            
            Search: <input ng-model="query">
          </div>
          <div class="col-md-10">
            
            <ul class="phones">
              <li ng-repeat="phone in phones | filter:query">
                {{phone.name}}
                <p>{{phone.snippet}}</p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    



