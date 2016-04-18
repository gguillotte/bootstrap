# Bootstrap CSS/JS for [docs.puppet.com](https://docs.puppet.com)

The docs.puppet.com site is built from the [puppetlabs/puppet-docs](https://github.com/puppetlabs/puppet-docs) repo, but it uses [Bootstrap](http://getbootstrap.com/) in its templates to reduce our maintenance load. And since the most efficient way to customize Bootstrap's CSS is to change the Less source, we've found ourselves maintaining a private fork.

To keep it focused, we've deleted most of the "real" branches of the Bootstrap source, and repurposed `master` for the canonical "live" code used in the puppet-docs site. At the time of this writing, the docs site fork was based on the `v3.3.6` tag from [the core Bootstrap repo](https://github.com/twbs/bootstrap).

## Updating Bootstrap in the docs site

We don't automatically compile Bootstrap from source as part of our build steps! The puppet-docs repo contains a compiled, minified version of Bootstrap in its `source/files/` directory. (The subdirectories mirror those in Bootstrap's `dist` directory.)

So if you make Bootstrap changes, you'll need to manually check the results into the puppet-docs repo. It goes a bit like this.

1. Clone this repo, and make sure you can build it.
    * Install Node.js with Homebrew. (Make sure you run `brew update` or whatever first.)
    * Follow [the instructions on the Bootstrap site](http://getbootstrap.com/getting-started/#grunt) for setting up Grunt and the build kit.
2. Make your changes to Bootstrap.
3. Build Bootstrap, copy it into puppet-docs, build+serve the site locally, and make sure everything works.
    * You'll probably only need to run `grunt dist-css` instead of `grunt dist`, because so far we don't make a habit of tweaking the Javascript sources.
    * Likewise, you'll probably only have to copy the contents of `dist/css` into `puppet-docs/source/files/css`.
4. Repeat 2 and 3 as needed.
5. Commit your BS changes and get them merged into master here.
6. Build one last time, copy the results into puppet-docs, and commit there. **Make sure you reference the Bootstrap commit SHA in your puppet-docs commit message!** Since everything's minified, it's the only easy way of tracking what's in the site.
7. Get your puppet-docs commit merged into master. If necessary, merge master into the pe-preview branch.

