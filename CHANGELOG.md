## 2021-02-24

### Changes

#### UI

* Using the Enter key to submit uploads or tag edits now shows a warning
  that you should use Ctrl+Enter instead.

* Adjusted input boxes to be a bit bigger in some places, to fit better on
  smaller screens, and to more consistently sized throughout the site.

#### Colors

* Changed colors in light mode to have better contrast and be more consistent
  throughout the site.

* Changed username colors (in light mode, if you have colored usernames turned on):
** Gold users are now orange.
** Moderators are now green.
** Builders are now purplier.
** Admins are now darker red.
** Username colors now use the same colors as tag colors.

* Parent/child borders are now darker green and darker orange.

* Changed the current post in the parent/child box to have a darker background,
  to make it easier to see.

* Changed how the New/Approved/Pending/Rejected labels look in the forum.

* Changed how the post mode menu indicates the active mode (for tag script
  mode, etc). Instead of giving the page a different background color, the post
  is highlighted when you hover over it.

#### Related tags

* Moved the artist tag to the translated tags section.
* Removed the artist URLs from beneath the artist tag.
* Selected tags are now shown in bold with a checkbox, instead of highlighted
  in blue. This is so you can see the tag type of selected tags.

#### Notes

* Removed support for a few disused CSS properties.
* Made the monospace font slightly thicker.

#### Other

* Added Baraag upload support.

### Fixes

* Fixed Pixiv commentaries generating bad /jump.php URLs.
* Fixed the tag counter counting duplicate tags.
* Fixed it so that when users send a dmail to themselves, it won't get
  potentially marked as spam.
* Fixed spellcheck being disabled in the note edit box.
* Fixed "()" in page title when the post didn't have a copyright tag.
* Fixed `*_(cosplay)` tags with a single post having their tag count marked in red.

### API Changes

* You can now have multiple API keys.
* You can now see when your API keys were last used, how many times they've
  been used, and which IP address last used them.
* API keys can be restricted to only work with certain IPs or certain API
  endpoints.
* If you're an app or script developer, and you have an app that requests API
  keys from users, you're highly encouraged to request that users generate keys
  with only the minimum permissions necessary for your app to work.
* If you have a privileged account, and you run scripts under your account,
  you're highly encouraged to restrict your API keys to limit damage in case
  they get leaked or stolen.
* The login action (POST /sessions) no longer returns the `api_token` field.

## 2021-02-05

### Changes

* Removed the rule that new users couldn't upload in their first 7 days.
* Raised the max video length from 2:00 minutes to 2:20 minutes for video uploads.
* Changed the post vote buttons to work the same way as the comment vote buttons.
* When aliasing or renaming an artist, the artist's {{\*\_(style)}} tag is now 
  moved too, if the artist has one.

### Fixes

* Fixed an error when searching for {{-status:any}}.
* Fixed @-ing yourself in a comment or forum post sending you a notification dmail.
* Fixed buggy keyboard movement of notes.
* Fixed the tag 'History' link not showing up on post search pages when the
  search contained a metatag.

## 2021-01-23

### Changes

* Changed 'Shortlink' to 'Copy ID' in comment menu.

### Fixes

* Fixed favorite icon not being filled in on favorited posts.
* Fixed series pool titles not being purple.
* Fixed bug when a logged out user tried to logout again.

## 2021-01-22

### Changes

* Comment system overhaul:

  * Comment scores are now visible.
  * The upvote and downvote buttons are now arrows.
  * `[quote]` tags have a new appearance.
  * The [Comments](https://danbooru.donmai.us/comments) page now shows 20 posts per page (before it was 5 posts per page).
  * The comment report/edit/delete options are now hidden behind a menu.
  * The comment menu has a "Shortlink" option that copies a comment #1234 link to the clipboard.
  * Removed the rule that regular Members couldn't post more than 2 bumping comments per hour. Now there's no limit on the number of bumping comments you can post per hour.
  * Removed the rule that you couldn't upvote your own comments.
  * The way hidden comments work has changed. Now when comments are hidden, instead of being hidden completely, they're replaced with a [hidden] link that you can click to unhide the comment.
  * The way deleted comments work has changed. Now when comments are deleted, they're replaced with a [deleted] placeholder, so you can see when a post has deleted comments.
  * The default comment threshold has been lowered to -8. This means that comments are now hidden when their score is -8 and greyed out when their score is -4. You can edit your settings to change your threshold back. Note that a threshold of -1 in the new system is the same as a threshold of 0 in the old system. So don't set it back to 0, set it to -1. Also, the max threshold is now 5 and the minimum threshold is now -100.
  * Mods can now click the comment score to see the list of voters.

* Account settings:

  * Removed the option to disable the next/previous post navbar under posts.
  * Removed the option to disable keyboard shortcuts.
  * Removed the option to disable tag autocomplete.

* The next/previous post navbar is now available to logged out users. This is the navbar beneath posts that lets you move to the next or previous post in a tag search. Previously this was only available to logged in users.
* You can now see the list of comments and forum posts you've reported to the moderators at [Moderation Reports](https://danbooru.donmai.us/moderation_reports).

### API Changes

* Deleted comments now have some of their fields hidden in the API. The creator_id, updater_id, and body fields are hidden if you're not a moderator.
* The `POST /comment_votes` and `DELETE /comment_votes` endpoints now return a comment vote instead of a comment.
* The `score` param in the `POST /comment_votes` endpoint now takes the values "1" or "-1", not "up" or "down".

Full changelog: https://github.com/danbooru/danbooru/compare/production-2021.01.13-021402-utc...production-2021.01.23-063752-utc

## 2021-01-12

### Changes

* Using the Enter key to submit an upload or save a tag edit will be removed
  in the future. Ctrl+Enter should be used instead (issue #4661).

* Added a new Restricted user level. New users start out as Restricted if they
  signup from a proxy or are detected as a sockpuppet. Being restricted is like
  a soft ban: you can't upload, edit tags, create comments or forum posts, or
  otherwise make any changes to the site, but you can still keep favorites,
  saved searches, and other personal things. Restricted users must verify
  their email address to become unrestricted.

* The Restricted system actually existed before, the only change is that now
  it's a public user level instead of a hidden flag on someone's account.

* Your IP address, location, and browser version are now recorded when you
  login to your account. They're also recorded when you create an account, or
  do any sensitive account actions, such as changing your password or email
  address, requesting a password reset, or deleting your account. Failed login
  attempts to your account are also recorded. Mods will be able to view this
  information. This information is recorded for account security purposes and
  for site moderation purposes (detecting sockpuppet accounts and ban evasion).

### Fixes

* Fixed a bug with not being able to upload certain Hentai Foundry posts (issue #4657).
* Fixed a bug with tag scripts sometimes adding the [[null]] tag (issue #4663).
* Fixed various issues with wiki other names, artist other names, and saved
  search labels allowing invalid characters.
* Fixed slow autocomplete when searching for Japanese or other non-English text.

### API Changes

* As described above, there's a new Restricted user level. Anything dealing
  with users will need to deal with a new user level.

* Added support for the following types of searches:

  * `<field>_not` searches on enum fields:
    * <https://danbooru.donmai.us/mod_actions?search[category_not]=post_regenerate,post_regenerate_iqdb>
    * <https://danbooru.donmai.us/mod_actions?search[category_id_not]=40..50>
    * etc

  * `<field>_<eq|not_eq|lt|gt|lteq|gteq>` searches on foreign key fields (user IDs, post IDs, etc):
    * <https://danbooru.donmai.us/comments?search[post_id_lt]=100000&group_by=comment>
    * <https://danbooru.donmai.us/comments?search[creator_id_not_eq]=502584&group_by=comment>
    * etc

  * `any_<field>_matches_regex`, where <field> is an array field:
    * <https://danbooru.donmai.us/wiki_pages?search[any_other_name_matches_regex]=^blah>
    * <https://danbooru.donmai.us/artists?search[any_other_name_matches_regex]=^blah>

  * Using multiple search filters on the same field. Before things like this didn't work:
    * <https://danbooru.donmai.us/tags?search[post_count_gt]=100&search[post_count_lt]=200>
    * <https://danbooru.donmai.us/comments?search[post][rating]=s&search[post_tags_match]=touhou>

# Past releases

* <https://github.com/danbooru/danbooru/tags>
* <https://danbooru.donmai.us/forum_posts?search[creator_name]=evazion&search[topic][title]=Danbooru+2+Issues+Topic>
