# Tabnabbing demo

Suppose you find an interesting link in a GitHub project README file and click on it.

<a href="http://molnarg.github.io/tabnabbing-demo/decoy_document.html" target="_blank">For the demo, click on this interesting link.</a>

For an explanation and a video, please scoll down.

.

.

.

.

.

.

.

.

.

.

## Screen capture

![Tabnabbing Demo](https://molnarg.github.io/tabnabbing-demo/tabnabbing_demo.gif)

## Explanation

* The link targets `_blank`, so it opens in a new tab.
* The JavaScript code running on the new tab has a handle to its opener tab (`window.opener`).
* The opened page navigates the opener to a phishing page that looks like a 'Timeout, please log in again' page on GitHub.
* The user closes the opened tab, and returns to what he thinks is GitHub.
* The user enters the credentials to log in again.

## Origin

Tabnabbing was first described by [Aza Raskin](https://twitter.com/aza) in a slightly different scenario
[here](http://www.azarask.in/blog/post/a-new-type-of-phishing-attack/).

## Possible solutions

Most sites don't care about this attack, Twitter and Google however does have a protection against it.
They don't open links in new tabs directly. Instead, they open a redirector page that sets `window.opener`
to null, and then redirects the user to the destination using JavaScript.

Opener is set to null automatically for links with `rel="noreferrer"`. Setting this on user provided links
provides protection against this kind of attack. The cost of this solution is that the referring site won't
show up as referrer in analytics on the referred sites.

Chrome developers say in [this bug report](https://code.google.com/p/chromium/issues/detail?id=45008#c1)
that "There isn't really anything to fix here. The hostname is the only authoritative identifier for a site".

IE (at least in version 11 and above) is protected against this kind of attack. The attempt
to change to opener window location is blocked by the popup blocker:

![IE behaviour](https://molnarg.github.io/tabnabbing-demo/ie.png)

