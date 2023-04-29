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
    - Based on the [Danger ruby gem](https://github.com/danger/danger).
    - Cloned the repository and [modified the gem](https://github.com/Winbobob/danger/compare/bff5e5e..1ccfed2) by adding the UUID and `cancel/confirm` instruct set support.
    - Updated the gemfile to [point to the customized Danger gem](https://github.com/expertiza/expertiza/blob/1422ae74d1d417164b0e68dd6e23de99393dd93f/Gemfile#L25).
    - Add the [dangerfile](https://github.com/expertiza/expertiza/blob/72fa52a0fab5f19e836205bbdae105b24f240fb9/Dangerfile) with system-specific guidelines.
    - [Setup TravisCI](https://github.com/expertiza/expertiza/blob/064b0b76e0acfe9ab89bc64180bc00aabf1748a7/.travis.yml#L43) to trigger the danger analysis everytime.
  - ParseHub
    - Based on an open-source tool named [TravisBuddy](https://github.com/bluzi/travis-buddy).
    - Cloned the repository and [modified the tool](https://github.com/Winbobob/travis-buddy/compare/961498..afe92bd) by adding handlers for different kinds of GitHub messages，for instance, `help` comments, `dispute` comments, `rerun` comments.
    - Deployed the tool as an http application to Heroku (free tier).
    - Setup GitHub webhooks to send request to the http application hosted on Heroku everyting there is a new comment added to any pull requests.
- Workflow
  - <img width="520" alt="Screen Shot 2023-04-29 at 12 57 19" src="https://user-images.githubusercontent.com/7702035/235321836-5af3797e-4dd6-40da-b100-cd7857a442dd.png">
  - Teaching staff or students create a comment on one GitHub pull request page (step 1).
  - GitHub will immediately notify the ParseHub via a webhook (step 2).
  - The ParseHub is used to (1) identify whether the comment includes a valid instruction set command, (2) parse the command and its parameters, (3) verify whether the current user is authorized to issue this command.
  - If the command is `dispute`, the ParseHub will trigger the bot (step 3) and the bot will notify the teaching staff on the GitHub (step 4) and send an email to teaching staff with a link to the dispute comment from the student (step 5).
  - If the command is `help` or unauthorized, the ParseHub will also trigger the bot (step 3) and the bot will simply add a new comment on the pull-request page with the available commands as the content (step 4).
  - If the command is `rerun`, `cancel`, or `confirm`, the ParseHub will trigger Travis CI through an API call (step 6). Then Travis CI will trigger the bot (step 7) and the bot will analyze the student code again and update its comment on GitHub pull-request page based on code changes, as well as cancellations and confirmations of guideline violations (step 8).
