---
class: post-blog post-detail
type: Blog
$title: "Ads on AMP pages became safer and more user-friendly in 2018"
id: ads-on-amp-pages-became-safer-and-more-user-friendly-in-2018
author: Vamsee Jasti
role:  Product Manager at Google, AMP Project
origin: "https://amphtml.wordpress.com/2018/12/11/ads-on-amp-pages-became-safer-and-more-user-friendly-in-2018/amp/"
excerpt: "In the past year, the AMP team took advantage of the latest browser features to keep users safe &#38; deliver a jank-free browsing experience. Because AMP powers billions of ads and pages on the web, these updates required no work from content creators or ad networks, making all AMP pages safer and faster for all [&#8230;]"
avatar: https://1.gravatar.com/avatar/42ecb1ea497ca9d0ffe1e406cae70e27?s=96&d=identicon&r=G
date_data: 2018-12-12T06:36:15+09:00
$date: December 12, 2018
$parent: /content/latest/list-blog.html
$path: /latest/blog/{base}/
$localization:
  path: /{locale}/latest/blog/{base}/
components:
  - social-share
inlineCSS: false
---

<div class="amp-wp-article-content">

		<p>In the past year, the AMP team took advantage of the latest browser features to keep users safe &amp; deliver a jank-free browsing experience. Because AMP powers billions of ads and pages on the web, these updates required no work from content creators or ad networks, making all AMP pages safer and faster for all users. Additionally we <a href="https://amphtml.wordpress.com/2018/12/06/contributing-to-webkit-for-a-more-predictable-web-platform/">directly funded</a> the implementation of the underlying security primitives in WebKit, so we’re happy to be able to extend the same security level to users of Apple’s Safari browser.</p><h2>Iframe Sandboxing FTW</h2><p>Iframe <a href="https://html.spec.whatwg.org/multipage/origin.html#sandboxing">sandboxing</a> allows web developers to set restrictions on iframe capabilities (e.g. the rendering of display ads). AMP now <a href="https://github.com/ampproject/amphtml/issues/14240">uses this feature</a> to sandbox all ads, eliminating attacks such as auto-redirecting which could previously be performed by ads.<br/></p><div class="wp-block-image"><figure class="aligncenter is-resized"><amp-img src="https://lh3.googleusercontent.com/VUW08FMqs0rs2mL4PZnRW3TSUJ6WxdEzrkHqkalC5d5bBWXHYDTnwW-BJrMoTFk5_FM_Tptv2PEOB2f40Is0R0N6lUK03QLxPDxIBEGRcgbJP5xTDU3wF0QiYkAy7WsFPROe2wyt" alt="" width="245" height="377" sizes="(min-width: 245px) 245px, 100vw" class="amp-wp-enforced-sizes"></amp-img><figcaption> An illustration of auto-redirect ads</figcaption></figure></div><p>A combination of ‘<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-top-navigation-by-user-activation">allow-top-navigation-by-user-activation</a>‘ and ‘<a href="https://html.spec.whatwg.org/#attr-iframe-sandbox-allow-popups-to-escape-sandbox">allow-popups-to-escape-sandbox</a>‘ attributes on the iframe gives web developers a practical way forward. It protect users on the primary site, while allowing the landing page to be functional.<br/></p><table class="wp-block-table"><tbody><tr><td><strong>Sandbox Feature</strong></td><td><strong>Description</strong></td></tr><tr><td>allow-top-navigation-by-user-activation</td><td>Ensures navigation from within an ad only happens on user action.</td></tr><tr><td>allow-popups-to-escape-sandbox</td><td>Removes any sandbox restrictions on the landing page of the ad.</td></tr></tbody></table><p>Initially users were only protected on Chrome. So we <a href="https://amphtml.wordpress.com/2018/12/06/contributing-to-webkit-for-a-more-predictable-web-platform/">funded</a> Igalia to add these features (<a href="https://bugs.webkit.org/show_bug.cgi?id=171327">link</a>, <a href="https://trac.webkit.org/changeset/219797/webkit">link</a>) and <a href="http://frederic-wang.fr/amp-and-igalia-working-together-to-improve-the-web-platform.html">many others</a> to WebKit, Safari’s open source browser engine. All users on Safari, Chrome and other browsers that support the underlying sandbox primitives (about <a href="https://www.statista.com/statistics/263517/market-share-held-by-mobile-internet-browsers-worldwide/">75% of mobile web usage</a>) are protected from auto-redirects. </p><h2>Aggressively Deprecating Synchronous Requests</h2><p><a href="https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Synchronous_and_Asynchronous_Requests#Synchronous_request">Synchronous requests</a> are bad for user experience because they can completely block all user interaction with a page until the network request succeeds or fails.<br/></p><div class="wp-block-image"><figure class="aligncenter is-resized"><amp-img src="https://lh6.googleusercontent.com/3AP1NBaTtS1FqCwKTE2VUY4nsOrO4TjerC82aOjHfQ66ImG_-PQ7Uss-CwQ0JpLquOQ7Pis8N2lgd4CTbem8VqBiYNoUR8hegtzOIUqFqS-oWwMpPhifS5gW9Z5FuJY14QKVOhiN" alt="" width="285" height="438" sizes="(min-width: 285px) 285px, 100vw" class="amp-wp-enforced-sizes"></amp-img><figcaption>     An illustration of a ‘sync-xhr’ side effect</figcaption></figure></div><p>Since display ads don’t pay for the externality (e.g. web page jank) they create, they have no incentive to write the most efficient code. Not only does this result in a bad page experience, this opens up a bad vulnerability that could help the ad creator. The most obvious way to drive up <a href="https://digiday.com/media/wtf-viewability/">viewability</a> of an ad is to fire off some heavy synchronous requests as soon as the ad gets into the viewport. This results in the ad creator earning better viewability while the page experience suffers dearly.<br/></p><p>Thankfully, Chrome <a href="https://www.chromestatus.com/feature/5154875084111872">now allows a feature policy</a> called ‘control Synchronous XMLHttpRequest’ that allows deprecating sync XHRs on iframes.</p><p>AMP <a href="https://github.com/ampproject/amphtml/issues/13766">launched</a> this feature policy for all ads served to AMP pages. We are also experimenting with implementing this for all iframes on AMP pages.</p><h2>Scaling Impact with AMP</h2><p>Millions of content creators have published AMP pages so far and 100+ ad networks have integrated with AMP. We’ve been able to roll out these changes to hundreds of millions of users without any new work from the content creator or the ad network. All it took was a few lines of code submitted to AMP’s open source <a href="https://github.com/ampproject/amphtml">repo</a>. <br/></p><p>One of the less obvious advantages of AMP is its ability to keep up with the latest browser features and automagically bring the entire ecosystem running on the safest &amp; most user-friendly slice of the web. For a website owner, a one time investment in AMP provides ongoing dividends.  <br/></p><p>It’s a humbling opportunity to advance the web at this scale, make it safe and deliver an excellent user experience for everyone. What are some other features that we can ship to a large part of the internet in 2019? <a href="https://github.com/ampproject/amphtml/issues/new">Let us know</a>.<br/></p><p><em>Posted by Vamsee Jasti, Product Manager at Google, AMP Project</em><br/></p>	</div>

	

</div>
