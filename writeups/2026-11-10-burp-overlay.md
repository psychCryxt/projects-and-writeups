# The Article Was Already on My Screen: Getting Past a Subscribe Overlay with Burp Suite

*November 10, 2026*

## The situation

This morning I was reading an article about how to become a great SOC analyst as a beginner. Halfway down the page, it blocked me: subscribe, or enter your email address, before you can read the rest.

Normally I don't fight this. I just use an email address I don't personally use, in case it ends up on marketing lists. But this time a different thought came: the article is *already loaded in my browser*. Is this gate actually holding anything back, or is it just standing in front of it?

## What I tried first

Developer tools. I inspected the page, dug through the sources and the network tab, and tried to remove the block from there. It didn't come out cleanly.

## Then I remembered Burp

I switched to Firefox, turned on FoxyProxy, and opened Burp Suite with intercept on. Now I could watch the page's requests one by one as they tried to leave my browser.

I let the request for the page itself through. I already had the article rendering. When the request for the overlay came, I simply didn't let the rest of the traffic go through. The gate never got its chance to stand up. Then I saved the page as a PDF and read the whole article in peace, no hassle.

No screenshots for this one: Burp's free (Community) edition doesn't save your work, and I had already closed it. And honestly, a screenshot would name the website, which was never the point. The point is the technique and what it teaches.

## What I learned

- **A client-side overlay is not access control.** The content had already been delivered to my machine; the "gate" was cosmetic, a curtain, not a lock. Anything enforced only inside the visitor's browser is controlled by the visitor.
- Real paywalls are enforced on the **server**, where the content genuinely never reaches you until you qualify.
- This is a lesson I want to keep as I learn security: when you assess a control, ask *where* it is enforced. If the answer is "on the client," it is a suggestion, not a boundary.
- And personally: this was the first time I solved something like this entirely on my own. No tutorial, no searching for the answer, no asking for help. I took pieces I had learned at different times (DevTools, proxies, Burp intercept) and branched them together into something new. That felt good, and it's exactly the thinking I keep hearing SOC work requires.

## Tools used

- Firefox with FoxyProxy
- Burp Suite Community Edition (intercept)
- Print/save to PDF for reading
