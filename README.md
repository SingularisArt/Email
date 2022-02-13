# Email

> NOTE: I'M NOT THE ORIGINAL AUTHOR. I GOT THIS IDEA AND MOST OF THE CODE FROM
> [THIS](https://github.com/ceuk) GUY. [HERE'S](https://github.com/ceuk/mutt_dotfiles)
> THE ORIGINAL REPO

## Some Features

* Query and save contacts via abook, goobook or ldapsearch (e.g. for Office365
  accounts, query only)
* Good calendar invite handling: render calendar invites inline and respond to
  them with `A` when viewing the calendar invite attachment
* Threads also contain emails sent by you like you see in modern email clients
  (this is achieved via notmuch)
* Nice handling of inline text/html rendering (use `C-l` to open up all links the
  email - great for quickly finding unsubscribe links)
* Secure configs (no hardcoded passwords etc)
* Fast global search of all mail in every account or all mail in a single
  account via NotMuch
* Everything looks really nice :)
* Includes all peripheral configs for isync, msmtp, notmuch etc

> NOTE: If you want to have all of the best features, including an automatic installation,
> then you're going to need my
> [dotfiles](https://github.com/SingularisArt/Singularis) (or whatever is
> needed)

## Setup

Just run: `./script`

Then, go in each folder's configuration and modify as needed

## Dependencies

* NeoMutt (latest version, all compile options enabled)
* [html2text](https://pypi.org/project/html2text/) (nicer HTML email rendering)
* [glow](https://github.com/charmbracelet/glow) (nicer HTML email rendering)
* Lynx (render HTML emails, W3m works well too)
* Notmuch (for email search)
* Isync (for syncing emails via IMAP)
* MSMTP (for sending emails via SMTP)
* python-vobject (for interacting with calendar invites)
* python-icalendar (for interacting with calendar invites)
* python-pytz (for interacting with calendar invites)
* python-tzlocal (for interacting with calendar invites)
* DavMail (if you want to use Office365/Outlook mail and the company locks down
  IMAP access)
* openldap (for using ldapsearch if you want to look up contacts on office365
  etc - required DavMail)
* abook (basic contact management)
* goobook (if you want to use google contacts instead)
* gcalcli (if you want to import events into a google calendar)
* urlscan (to quickly show/open links within an email)
* pandoc (if you want to compose HTML emails in markdown)

## Contents

* `bin/import_calendar_invite` - imports a calendar invite into google calendar
  with gcalcli and then calls mutt-ical to respond to the invite
* `bin/ldap_owa_query` - allows contact searching via LDAP (used for coroprate
  office365/outlook accounts)
* `bin/mailsync` - a great script that syncs your mail, originally written by
  Luke Smith
* `bin/mutt-ical` - used to respond to email calendar invites
* `bin/mutt-trim` - clean up emails when quoting reply
* `bin/mutt-nm-search-cached` - search emails with notmuch
* `bin/render-calendar-attachment.py` - used to render email calendar invites
  in Mutt
* `bin/mutt-viewical` - used to render ical attachments in Mutt
* `bin/beautiful_html_render` - best approach I've found so far
* `isync/mbsyncrc` - configuration file for isync (used to sync your emails).
  There are examples of many different account types to use as a starting point
* `glow/*` - various settings and themes related to Glow
* `msmtp/config` - configuration file for msmtp (used to send emails). There
  are examples of many different account types to use as a starting point
* `mutt/accounts/*` - individual config files for each email account you wish
  to use in Mutt. There are examples of many different account types to use as
  a starting point
* `mutt/muttrc` - the main Mutt config - use this to customize various
  settings/macros/bindings etc
* `mutt/styles.muttrc` - my custom styling for Mutt - you shouldn't need to
  tweak this much/at all
* `mutt/mailcap` - mailcap file for detrening how to render different types of
  emails/attachments - customize as needed (there's already quite a lot of
  handy stuff in there)
* `notmuch/notmuchrc` - config file for notmuch (used for searching emails) -
  you will need to change some values in here such as your name/email
* `systemd/user/calendar-remind*` - systemd timer/service files for repeatedly
  calling gcalcli remind (to generate notifications 15 mins before an event
  starts). Enable with systemctl --user enable calendar-remind.timer or delete
  if you don't need.
* `systemd/user/gcalcli*` - systemd timer/service files for repeatedly calling
  gcalsync (to sync gcalcli with google calendar). Enable with systemctl --user
  enable gcalcli.timer or delete if you don't need.
* `systemd/user/mailsync*` - systemd timer/service files for repeatedly calling
  mailsync (to sync your emails). Enable with systemctl --user enable
  mailsync.timer
* `systemd/user/vdirsyncer*` - systemd timer/service files for repeatedly
  calling vdirsyncer sync (to sync your calendars). Enable with systemctl
  --user enable vdirsyncer.timer
* `vdirsyncer/config` - example configs for vdirsyncer (used to sync calendars,
  I recommend using with [Khal](https://github.com/pimutils/khal))

## Key Bindings

All default keys are unbound to remove random, unwanted bindings and commands.
Therefore all bindings are explicit.

> NOTE: These key mappings may not be 100% accurate. Please view the latest
> mappings [here](mutt/keys/binds.muttrc).

Press `?` inside Mutt to see available keybinds for your current context.

### General

* `q`:        Exit/close/back
* `<Esc>`:    Abort command
* `?`:        Help
* `/`:        Search
* `j`:        Scroll down
* `k`:        Scroll up
* `gg`:       First item/top
* `G`:        Last item/bottom
* `<Return>`: Open/select/confirm
* `<Tab>`:    Trigger auto-complete
* `n`:        (when searching) search next
* `N`:        (when searching) search previous
* `Ctrl-u`:   Scroll half a page upwards
* `Ctrl-d`:   Scroll half a page downwards
* `Ctrl-n`:   Next unread message
* `Ctrl-p`:   Previous unread message
* `zz`:       Center screen on current selection (similar to Vim)
* `zt`:       Center screen at top of current selection (similar to Vim)
* `zb`:       Center screen at bottom of current selection (similar to Vim)
* `d`:        Delete email
* `u`:        Undelete email
* `U`:        Undelete thread

### Responding to Emails

* `r`:        Reply to email
* `R`:        Group reply email
* `F`:        Forward the email

### Index-specific

* `gi`:       Go to inbox
* `Mi`:       Move email(s) to inbox
* `Ci`:       Copy email(s) to inbox
* `gs`:       Go to sent
* `Ms`:       Move email(s) to sent
* `Cs`:       Copy email(s) to sent
* `gd`:       Go to drafts
* `Md`:       Move email(s) to drafts
* `Cd`:       Copy email(s) to drafts
* `gp`:       Go to spam
* `Mp`:       Move email(s) to spam
* `Cp`:       Copy email(s) to spam
* `ga`:       Go to all mail
* `Ma`:       Move email(s) to all mail
* `Ca`:       Copy email(s) to all mail
* `gl`:       Go to a specific folder
* `m`:        Move email(s) to a specific folder
* `Ctrl-a`:   Mark all messages as read
* `*a`:       Select all emails
* `*n`:       Deselect all emails
* `*r`:       Select all read emails
* `*u`:       Select all unread emails
* `s`:        Star/unstar email
* `U`:        Marked as unread
* `I`:        Marked as read
* `<Return`:  Display message
* `#`:        Mark as complete
* `Ctrl-i`:   Limit by flagged
* `O`:        Sync all mail
* `Ctrl-l`:   Call **urlscan** to open links
* `s`:        Save email(s) to ~/Downloads
* `h`:        Go to parent folder

### Composing Emails

* `y`:        Send composed email
* `a`:        Attach file(s)
* `p`:        Postpone message (save to draft)
* `e`:        Edit email
* `t`:        Edit "to" field (recipient)
* `f`:        Edit "from" field (sender)
* `s`:        edit subject
* `c`:        edit "CC" field
* `b`:        edit "BCC" field
* `r`:        Rename email
* `F`:        Filter entry
* `Ctrl-t`:   Edit type
* `<Return>`: View attachments

### Tagging emails

* `t`:        Tag entry
* `T`:        Tag thread
* `<Space>`:  Flag email
