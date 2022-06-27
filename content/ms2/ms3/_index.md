---
title: "Milestone 3 - Future Features"
weight: 1
# geekdocFlatSection: false
# geekdocToc: 6
# geekdocHidden: false
---
This page documents our planned extension features to be done for Milestone 3.

# Frontend

1. User experience
   - Responsive page design for use with mobile and tablet
   - SMS/Email (un)subscription for backend [lookout service](#lookout-service)
2. Geocoding
   - Implement geocoding with Google Maps API, which translates user input into GPS coordinates
   - Integrate map into application and allow user to view item location and get directions
3. Application Testing
   - Extend unit and integration testing to cover all components and pages
   - End-to-end testing with <a href="https://www.npmjs.com/package/puppeteer" target="_blank" rel="noopener">Puppeteer</a> to simulate user intertaction with application

# Backend
1. Lookout Microservice <div id="lookout-service"></div>
    - When a loster submits a lost item, lookup the found database to see which items potentially match the lost item
    - Asynchronously send a 'possible match' alert to the Lost user 
    - Possible utilisation of a NLP library to optimise lookups for more relevant matches
2. Security Hardening
    - Add authentication guards to various priviledged endpoints
    - Simple DDoS mitigation logic
3. Include GPS/Geographical data in Database Schema to assist in Geocoding feature

# Extended Documentation
1. User guide
2. Developer guide & contribution docs