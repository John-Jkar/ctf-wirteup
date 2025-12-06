**s1mple**
490
web easy

Author: mrbgd

"My aim is for my team to be number one, the rest is irrelevant". Anyway, is s1mple that simple? I'm gonna go watch the CS2 major, hope you don't ruin anything pls
**URL**
http://public.ctf.r0devnull.team:3023/

**Method of Solve**
This was a web challenge where we were given a login form to login as admin. On recon I found out that that the password field was vulnerable to sql injection
~~~
**Login credentials**
Atmin
' OR '1'='1  - sql injection payload
~~~
After login I was taken to admin dashboard where there was a search field and it was vulnerable to ssti on testing with {{7*7}}.

**Payload used**
{{ self._TemplateReference__context.cycler.__init__.__globals__.os.listdir('/app') }}
