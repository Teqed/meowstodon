# Meowstodon

## Introduction

This Mastodon fork is based on the [Catstodon Fork](https://github.com/CatCatNya/catstodon) which is based on the [glitch-soc Fork of Mastodon](https://github.com/glitch-soc/mastodon), with changes made to suit [shatteredsky.net](https://shatteredsky.net).

To install, take a look at [glitch-soc.github.io/docs/](https://glitch-soc.github.io/docs/), substituting this repository where appropriate.

## glitch-soc - Differences from mastodon/mastodon
The following is an excerpt from [glitch-soc's documentation](https://glitch-soc.github.io/docs/):

- Media improvements
- Images inside the CW spoiler
- fullwidth images
- scaling options
- Formatted toots
- Highlighting of misleading links
- Hiding follower count
- An app settings modal
- Collapsible toots
- Colored toot visibility icons
- Local-only toots
- Threaded mode
- data-* attributes on statuses for custom CSS targeting
- Advanced theming via flavours+skins
- Doodle

## Catstodon - Differences from glitch-soc

- Emoji reactions on statuses (with both Unicode and custom emojis, same as for announcements).
- The web frontend emoji picker is a blobcat instead of the joy emoji.
- The rate limits for authenticated users have been relaxed a bit.
- The API endpoint `/api/v1/custom_emojis` is no longer affected by AUTHORIZED_FETCH, allowing anyone to copy custom
  emojis.
- Allow higher resolution images. (4096x4096 instead of the previous limit of 3840x2160)
- Allow posting polls with only one poll option (if `MIN_POLL_OPTIONS` is set to 1 on your instance).
- Added oatstodon flavour (by [@oat@hellsite.site](https://hellsite.site/@oat))
- Some sound files are adjusted:
  - sounds/boop.mp3
  - sounds/boop.ogg
- Emoji reactions on statuses (with both Unicode and custom emojis, same as for announcements), a feature originally
  developed for [Nyastodon](https://git.bsd.gay/fef/nyastodon).
  Ended up as a Catstodon-maintained patch after its initial two Pull Requests to glitch-soc, but was handed over
  to [Essem's fork, Chuckya](https://github.com/TheEssem/mastodon) and is now
  pending [its fourth attempt of merging into glitch-soc](https://github.com/glitch-soc/mastodon/pull/2462).
- Lifts the "only federate local favourites" restriction on favourites/likes and emoji reactions.
- Cherry-picks the
  [activity filter branch](https://github.com/chikorita157/mastodon-sakura/tree/newmain-tmp3-noellabo-filtering)
  from [Sakurajima Mastodon](https://github.com/chikorita157/mastodon-sakura).
- Adds the ability to disable the suspicious sign in detection entirely.
  - Useful for situations where the instance may not have up-to-date IP information, such as when the period of IP
    address retention is set to a low value (see _Previous differences now merged into vanilla Mastodon_)
- Environment variable `MASTODON_USE_LIBVIPS` is true by default.
  - This is a minor change, but it _requires_ all systems running Catstodon to run a recent libvips version (8.13+).
  - Vanilla Mastodon intends to deprecate ImageMagick anyway, so sooner or later, this change will cease being one.
- Allow dashes in emoji shortcodes
  - This is simply to allow custom emoji compat with other fedi software.
  - Original patch by hazycora: https://github.com/TheEssem/mastodon/commit/2dde7a25a47a23f827e2fd2d07f55438f9985181

## Meowstodon - Differences from Catstodon

- Emojis enlarge on hover (thanks to [@neatchee's glitch-soc fork](https://github.com/neatchee/mastodon/tree/feat/enlarge_emoji_on_mouseover_option))
- Counters in the web interface [have been modified](https://github.com/Teqed/meowstodon/blame/15b5e3eb79607ce1f01fb6ba0b16ebed5ab97a5b/app/helpers/home_helper.rb) to display `count` or `ShortNumber` instead of `1+`.
- The queries for trending statuses [have been changed](https://github.com/Teqed/meowstodon/blame/15b5e3eb79607ce1f01fb6ba0b16ebed5ab97a5b/app/models/trends/statuses.rb) -- instead of using `recently_used_ids()` a selection of recent statuses from the last week are chosen.
- When [calculating scores](https://github.com/Teqed/meowstodon/blame/15b5e3eb79607ce1f01fb6ba0b16ebed5ab97a5b/app/models/trends/statuses.rb) for trends, set `allowed = true` for eligible statuses.
- [Personal rel="me" headers](https://github.com/Teqed/meowstodon/blame/15b5e3eb79607ce1f01fb6ba0b16ebed5ab97a5b/app/views/layouts/application.html.haml) added for link verification of alt profiles. Currently hardcoded but in the future this might be provided by environment variable -- change these if forking.

## Previous differences now merged into glitch-soc

- Fixed incorrect upload size limit display when adding new a new custom
  emoji. ([Pull request](https://github.com/glitch-soc/mastodon/pull/1763))
- Everything merged into vanilla Mastodon

## Previous differences now merged into vanilla Mastodon

- The period of retention of IP addresses and sessions was made
  configurable. ([Pull request](https://github.com/mastodon/mastodon/pull/18757))
