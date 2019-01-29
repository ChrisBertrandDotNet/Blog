# How to stop security tools from killing the open-source software movement
(2019-01-24)

![](How%20to%20stop%20security%20tools%20from%20-%20AVs.png)

# What is happening ?
Security tools now all apply the same principle: when they find an _unknown_ software (or version), they alert the user, usually displaying scaring messages such as:
> “A suspicious program has been detected ! It has been blocked and placed in quarantine”.

Recently, some security tools slightly evolved and give a bit more information:

> “A suspicious program has been detected. Rare software are usually virus. So it has been blocked.”

Follows a big button “OK” that accepts destroying the “suspicious” software.  
And, in tiny characters, a short link says “More details”. Of course this link leads to the real options: let the security tool destroy the software, or trust the software.
## Put yourself in the shoes of a software author
As a software author, let me tell you how disastrous can be this scheme.

Imagine you create a software, an application for desktop computers, for example.  
It can be open-sourced, or free or paying, whatever.  
After a few weeks, months or years, you proudly publish it.  
Immediately, you receive emails :  
> “Hello  
When I download your software, my security tool tells me it’s a virus and deletes it.  
Is it a malware ?”         [ Isn't it a lovely naive question ?   ;-)   ]

Others say:
> “I extracted the files from the Zip, then ran the application.
But my security software blocked it saying it’s probably a virus.
What can I do ?”

At this moment, you have to patiently explain that
> “No, it's definitively not a virus. You can bypass the blocking by clicking on _More information_ then _Trust software_, etc.”.

Of course, you need to know all security tools in order to give a different procedure to every user.

Then you have to contact every security company and, patiently again, explain that you _swear_ your software is not a virus, and convince them to trust it or to check it at least.  
Unfortunately, your software is only one of the thousands this company receives daily.  
After you did this unplanned work, maybe, if you are lucky, your software will pass security tools’ defences.

Victory !  
The kind of victory that costs a lot..

As you can imagine, some authors can be slightly discouraged by this unplanned work, especially when there is no money in return.
## The gods _Signature_ and _Code Signing Certificate_
Several years ago, in order to limit the virus plague, the security industry and the software industry (or at least some of the biggest companies) invented the concept of software _signature_.

Along with this concept, every software that is published should be _signed_ using a _code signing certificate_ owned by the author.  
Signing a software proves who is its author and certifies the software has not been modified after its release (it is “genuine”, it was not modified by a virus for instance).

In  order to sign a software, an author/company has to buy a code signing certificate to a _certification authority company_. The latter certifies who is the author of the signature by publishing the _public key_ part of the certificate so that security tools can check this signature at any moment.

The certification authority company serves as an independent and neutral assurance that certifies this signature is the genuine one, and not a fake one.

That explains why when you try to download or run unsigned software, your security tool warns you, while it does not (always) on signed software.

## Why programs are so rarely signed
Currently, the great majority of open-source authors do not sign their software.  
It’s probably due to the difficulties signature implies:  
- Certificates are quite expansive, 90 to 600 US$, and are paid annually.  
That is much money for a volunteer.
- Buying them implies a complex, rather long and boring identification process.
- Applying them implies a rather complex process (extracting keys, converting them, checking time stamping, etc.).

In addition, I note most software authors are not very familiar with signature, certificates, keys and security concepts. That can lead to do mistakes, such as ignoring important details (who knows the _Time Stamping Server_ ?).
## A disaster in the long run
After a few years, the way security tools behave has a great influence on the software industry, the software authors, and the open-source movement in particular.

Famous established software have no problem, because security companies know them, trust them and check every new version. Of course, famous software are rare, so it’s possible to pay more attention on them.

The same for small companies, assuming they earn money.

Now for starting tiny companies and open-source authors, the problem is different.  
As we saw, the signature process is both expansive and relatively complex. Who wants to spend money and time when there is nothing (or few) in return ?

The problem is small software are millions where famous software are a few hundreds only.

As security tools tend to block unsigned software now, they favour big software/companies.  
Small software authors, especially open-source and free software, are slowly and silently rejected from the software market.  
It’s a kind of filter that would say :
>“If you are big enough, you can sign, and we let you pass. Otherwise, you will disappear”.
# My proposal
I propose to use self-signed certificates.

They are very easy to generate, renew and manage, contrary to the regular certification authority certificates, and they are free.

The scheme :
1. Open-source authors create a self-signed certificate they then use to sign their products.  
That proves they are the author of their published products.
2. Security tools link every certificate to authors/companies, and evaluate new software (and new versions) in consequence.

That means the traditional “certification authority” is not necessary. Anyway, security tools can evaluate what signatures are genuine.  
I would say that, in general, when a program appears for the first time, we can be sure it contains the genuine signature.
## Do we need “certification authority companies” for software identification ?
Personally, I trust more the proposed scheme than the traditional scheme that implies trusting certification authority companies.  
Especially considering these companies concentrate so many keys, millions or billions, that they will always be the favourite target of all hackers/crooks/criminal-organizations/dark-administrations in the world.

With self-signed certificates, the private key stays secret.

In addition, I’m not much impressed by the identification process these companies apply when a customer buys a certificate. As they tend to simplify the process and make it faster, they facilitate fakes.  
I would not be surprised that criminals have no difficulty in faking identities, either inventing inexistent companies/people or even faking real companies.

Let me ask you a question:  
As a certificate is a kind of password, would you share your password with a company ? A company that stores millions of passwords ? A password that is the basis of the security of your products ?
## A tutorial would be welcome
I encourage companies/authors of security tools to publish a tutorial for software authors, that explains how they can properly create a self-signed certificate and apply it to their products.  
At the same time, this article should explain why such signatures are important to security tools/companies.
# Conclusion
Current security practices tend to reduce the right of free enterprise by means of questionable requirements.  
It's time to change the rules. Self-certificates are an easy and reasonable way to sign software and improve security.  
Security tools now have to behave consequently.