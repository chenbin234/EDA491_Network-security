# 3.1 [The Basics](http://manual-snort-org.s3-website-us-east-1.amazonaws.com/node2.html)

Snort uses a simple, lightweight rules description language that is flexible and quite powerful. There are a number of simple guidelines to remember when developing Snort rules that will help safeguard your sanity.

Most Snort rules are written in a single line. This was required in versions prior to 1.8. In current versions of Snort, rules may span multiple lines by adding a backslash \\ to the end of the line.

Snort rules are divided into **two logical sections**, **the rule header and the rule options.** The rule header contains the rule's action, protocol, source and destination IP addresses and netmasks, and the source and destination ports information. The rule option section contains alert messages and information on which parts of the packet should be inspected to determine if the rule action should be taken.

Figure illustrates a sample Snort rule.

<table><caption><strong>Figure:</strong> Sample Snort Rule</caption><tbody><tr><td><img width="423" height="34" src="http://manual-snort-org.s3-website-us-east-1.amazonaws.com/img29.png" alt="\begin{figure}\begin{verbatim}alert tcp any any -> 192.168.1.0/24 111 \
(con...
...\vert0 01 86 a5\vert''; msg:''mountd access'';)\end{verbatim}
\par\end{figure}"></td></tr></tbody></table>
**The text up to the first parenthesis is the rule header and the section enclosed in parenthesis contains the rule options. The words before the colons in the rule options section are called option keywords.**

**Note:**  

Note that the rule options section is not specifically required by any rule, they are just used for the sake of making tighter definitions of packets to collect or alert on (or drop, for that matter).

All of the elements in that make up a rule must be true for the indicated rule action to be taken. When taken together, the elements can be considered to form a logical AND statement. At the same time, the various rules in a Snort rules library file can be considered to form a large logical OR statement.