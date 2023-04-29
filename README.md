# Bot-With-Interactions-Improving-GitHub-Pull-Request-Feedback-Through-Two-Way-Communication

## Danger Bot
- Based on [a Ruby gem named Danger](https://github.com/danger/danger)
- Detect [more than 40 system-specific guideline violations](https://github.com/expertiza/expertiza/blob/main/Dangerfile)
- Programmable, extensible, and portable
- Danger Bot is more than a linting tools
- [Setup tutorial](https://github.com/Winbobob/Improving-Feedback-on-GitHub-Pull-Requests-A-Bots-Approach#:~:text=on%20your%20repo%3F-,Danger%20Bot,-Guides)

## Danger Bot 2.0
- Danger Bot + two-way communications
- [Use case](http://zhewe.me/blog/danger-bot-2-use-case)
- [Tutorial video](http://zhewe.me/blog/danger-bot-2-tutorial-video)
- Architecture
  - Danger Bot 2.0
  - 
  - ParseHub
   - Based on an open-source tool named [TravisBuddy](https://github.com/bluzi/travis-buddy)
   - Cloned the repository and [modified the tool](https://github.com/Winbobob/travis-buddy/compare/961498..afe92bd) by adding handlers for different kinds of GitHub messages，for instance, `help` comments, `dispute` comments, `rerun` comments.
   - Deployed the tool as an http application to Heroku (free tier)
   - Setup GitHub webhooks to send request to the http application hosted on Heroku everyting there is a new comment added to any pull requests 
