+++
date = "2016-06-21T04:03:46-06:00"
draft = false
title = "Standards"

+++

Standards are beautiful. Standards let us build on top of each other without worrying too much about details underneath. The biggest example of standard is probably human language, how we all agreed to make specific sounds so that we'll be able to express ourselves to each other.

I like to think in standards. Whenever I'm creating something, I worry a lot thinking how can someone else leverage the work that I'm working. I think this way of thinking and building the little programs we build not only help others, but ourselves more because we no longer need to worry about integrations. Integrations are a given when everyone agrees. The world moves on.

I have built a boilerplate application for those who are building APIs from scratch. If I had to pick out one thing that I had most fun in building this was how I learned to build on top of standards. One exampleis how JSON schema has been used to define database model, while the same schema is used to generate seed data. I also embedded the JSON schema on the API documentation because the documentation library also understands how to deal with JSON schema standard.

I was able to feed a single file to three different module of the project because all of them understood the standard.

