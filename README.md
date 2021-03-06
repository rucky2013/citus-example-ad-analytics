## Citus Example: Ad Analytics

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/citusdata/citus-example-ad-analytics)

Example app that uses the distributed Citus database to provide a realtime ad analytics dashboard.

You can see the deployed version at http://citus-example-ad-analytics.herokuapp.com/

## Deploying on Citus Cloud and Heroku

1. Signup for a Citus Cloud account: https://console.citusdata.com/users/sign_up
2. Provision a new formation of servers (they are billed hourly), a small one is good for testing
3. On the formation detail page, wait until the cluster is configured, then click *Show Full URL* and copy it to your clipboard<br>
<img src="http://f.cl.ly/items/13453P1H3g3o19272S0e/Screen%20Shot%202016-06-05%20at%209.51.05%20PM.png" width=400" />
4. Click the "Deploy to Heroku" button and enter the URL from your clipboard as `DATABASE_URL`:<br>
<img src="http://f.cl.ly/items/071U2k270Q3y0u0G1V1q/Screen%20Shot%202016-06-06%20at%2012.24.54%20AM.png" width="400" />
5. Run `heroku run:detached rake test_data:load_bulk` to load sample data - this will take a while

After starting the data load task visit the app to see an example of what you can build with Citus.

Note: If you get an error like "could not find the source blob" on Heroku deploy, just click the Deploy button again.

## Screenshots

<img src="http://cl.ly/0y430z3l122y/Screen%20Shot%202016-06-01%20at%206.15.02%20PM.png" width="600" />

## Schema Diagram

<img src="http://cl.ly/0n3G0Q453p1X/schema_diagram.png" width="600" />

We're distributing only the part of our dataset that we expect to take significant amounts of space, specifically
`clicks` and `impressions`.

We use `ad_id` as the common shard key for the hash distribution, in order to have data for a specific ad colocated on one shard.

## LICENSE

Copyright (c) 2016, Citus Data Inc

Licensed under the MIT license - feel free to incorporate the code in your own projects!
