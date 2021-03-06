FAQs
=

The following are some of the frequently asked questions. Please contact us with any other questions and if there is anything that you think should be on this list.

How long does it take for a message to arrive?
-
Your emails should arrive within seconds (actually we aim for it to be milliseconds). Our email server doesn't poll for your emails, they will be received as soon as they are sent to the server. A little bit of processing and they're sent straight on to your app.

How do I change the website that my email is posted to
-
The CloudMailin website allows you to view all of your email addresses and to change the target location. Click [here](http://cloudmailin.com/addresses) to view and edit your addresses.

How can I use my own domain name or email@mydomain.com instead of a CloudMailin address.
-
There are two ways to do this. The first is to use a [custom domain](custom_domains). This allows you to receive email on any account at the specified domain name.

If you only need a single address the easiest way to do this is to get your current email server to forward any mail sent to example@mydomain.com to your cloudmailin address.

Can I create a Wildcard DNS entry or subdomain for my Custom Domain?
-
Yes. Just make sure you create the DNS records first following [these](custom_domains) instructions. When you create your custom domain simply enter \*. in front of the domain name such as \*.example.com.

How can I give each of my users a unique email address to send to?
-
At the moment we recommend forwarding email from your own domain to your cloudmailin address in order to achieve this. You can then look at the message envelope to see which address the message was sent to.

You can also use a plus in your email address to create a disposable email address. Disposable email addresses allow you to use a unique email address for each user. As an example, a user given an email address in the form example@example.com could use example+something@example.com or example+1.2.3@example.com.

The disposable part of each address will be delivered as a paramater within the [post format](post_format).

What format will the message arrive in?
-
Your server will receive an HTTP POST to the url that you specify. This will be in the exact same format as if the user pasted the email into one of the fields of a multipart/form-data form on your website. For more details of the exact format please see the HTTP POST [documentation](post_format).

Great I've got the raw email but how to I get the content from it?
-
We send you the raw email so that your system can parse it the way you want it to. We do however pull out some basic info like the sender and subject to make life easier. There are loads of libraries out there to take the raw email and extract the contents. Take a look at [this](parsing_email) page for some examples.

Do you support attachments?
-
Sure, we send you the entire email in its raw form. Its up to you to get the attachment out of the email but there are plenty of tools to help you do this. Take a look at [this](parsing_email) page for some examples.

How robust is this service?
-
We have tried to make things pretty robust, in fact we should be far better than most email hosting systems, however everyone makes mistakes and sometimes things happen that are beyond our control.

We're not going to offer you one of those silly agreements that says something like 99% uptime (3 days a year is a long time!) instead we're going to promise to do our best. If the site goes down we will receive emails (ironic we know), SMS messages and hopefully a bunch of tweets! We will get cracking as soon as possible and work our socks off to bring the site back to life. If the server is unavailable, almost all mail servers will retry a little later anyway.

What happens if the server is unavailable?
-
Because of the way email and SMTP works most mail servers will try and resend your emails until the email is delivered or too many retries have occurred. We are considering adding a separate backup mail server to make sure this happens quicker but for now we are relying on the other server to resend the mail.

What if my site is down?
-
In exactly the same way that servers will retry if our system is down, the same will happen with your system. In fact we will respond to the following status codes or errors:

* If we can't reach your server. We will tell the user's mail server that there has been a temporary problem so try again later. This will be shown as 000 in the delivery status pages.
* If you give us an http status of *200* - Everything is good we will tell the mail server the message has been delivered
* If you give us an http status of *404* - The message will be rejected and the sender will be notified of this problem.
* If you give us an http status of *422* - The message will be rejected and the sender will be notified of this problem.
* If you give us an http status of *500* - we will tell the mail server to try again later.
* Any other status and we will also tell the mail server to try again later.

See the [HTTP Status Codes](http_status_codes) page for more details

How many times will a user's email server retry before it gives up?
-
This is entirely dependent on how the mail server was set up. However, most mail servers will retry often at first and then start to back off. In our experience Google for example will start by trying every 30 minutes then back off to once every 4 hours or so and will do this for about 4 days. They will also tell the user that the message delivery has been delayed.

How do I know that things are working?
-
We have built a simple delivery status system to allow you to see some basic details about the most recent messages we have received and tried to deliver to your site. Most importantly the HTTP status that your site returned is logged as part of this status. A status of 000 means we couldn't reach the server specified as the target.

How can I test things with a fake target?
-
We have wired up a few fake targets you can use to test your emails.

* http://cloudmailin.com/target/200 - will simulate a 200 response. This simulates the message successfully being delivered.
* http://cloudmailin.com/target/404 - will simulate a 404 response. This simulates your site not knowing anything about the page you have set as your target.
* http://cloudmailin.com/target/500 - will simulate a 500 response. This simulates something going wrong on your site and you asking the server to deliver the message later.

How can I reject messages and send a custom error message?
-
Certain HTTP status codes can be used to reject messages and alert the sender such as 403, 404 and 422.

If you give a status code that rejects the message such as 422, you can also set a message to go with it. Simply set the content type of this response to _text/plain_ and your HTTP response will be included in the error message sent to the server.

How can I see the response my server returned
-
On the address page within CloudMailin you should see the message and the status that your server returned to CloudMailin. Clicking on the details tab will also show additional information.
The details also include the first 2kb of any failed response so that you can determine what may have gone wrong with your server.

My server had a temporary problem and a message was delayed, how can I see if it was delivered?
-
You can use the details page for a delivery status to see all delivery attempts with the same message ID. Hopefully one of these is green.

I am receiving an error trying to create my custom domain?
-
You must make sure that your setup your DNS entries with either a CNAME or MX records pointing to CloudMailin before trying to enter a custom domain in the control panel. If you try to enter your custom domain first, it will fail to validate stating that the DNS records cannot be found. Take a look [here](custom_domains) for more information about setting up your custom domains.

Where are your server based?
-
Our servers predominantly based in EC2's US-EAST region (it is most likely these are the servers you will reach). This is to allow low latency and cut costs for the majority of our users. We do however make use of several other hosting providers to provide redundancy can add others upon request if required. Contact us for more details.