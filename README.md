# wercker-output-test

## Explanation

`wercker.yml` contains two pipelines: **build**, and **other-build**

Both pipelines contain the same steps:
`npm-install`
`npm run start`

- `npm run start` executes `gulp`

- `gulpfile.js` contains default step: `console.log('Some output should appear in all pipelines');`

Running `wercker build`, `wercker build --pipeline build`, and `wercker build --pipeline other-build` locally all result in displaying the expected stdout in the terminal. This is good :+1:

However, stdout seems to be suppressed on wercker.com for "chained pipelines"

### Issue

On wercker.com, pipelines can be triggered from a git push, or they can be chained to run after another pipeline finishes.

Again, the `wercker.yml` file in this project contains two pipelines: **build**, and **other-build**

[This wercker application](https://app.wercker.com/amougeot/wercker-output-test/runs) has a few pipelines defined:
- `build`: the default build pipeline)
- `other-build-triggered`: runs the `other-build` pipeline _on git push_
- `other-build-chained`: runs the `other-build` pipeline _chained to run after "build"_

Looking at the output from `other-build-triggered`, we see the expected stdout:
> Some output should appear in all pipelines

However, looking at the output from `other-build-chained`, we see the same command being executed, but no stdout output :(


[![wercker status](https://app.wercker.com/status/2772eb97d3656ebb99bfa955e5a1fc65/s/master "wercker status")](https://app.wercker.com/project/byKey/2772eb97d3656ebb99bfa955e5a1fc65)
