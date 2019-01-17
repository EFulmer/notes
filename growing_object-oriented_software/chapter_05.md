Chatper 5: Maintaining the Test-Driven Cycle
============================================

Some key principles:

* **When building a software, write outward in.** Write acceptance tests first. This helps both with understandinf the user's wants, and also by removing potentially incorrect assumptions about the specific tech needed. There's a recurring theme throughout the book of making your life as an engineer easier by frontloading the difficult work -- meaning making the most difficult parts at the outset. Rather than backloading this work, by scrambling and spending late nights and a lot of stress to automate deployment at the eleventh hour or fix a choice made by an incorrect assumption.
* **Start with the simplest success case possible.** Two big reasons for this. One is that it can be harder to envision possible failure cases. The second is that it's demoralizing to try to break a system that isn't even build yet.
* **Include very, very detailed error messages.** When something fails, there should be zero ambiguity as to where and how it failed. Obviously, this doesn't mean you should include API keys or other secure data in the logs, or a stack trace, but you should include everything that may be needed to trace the error at 11:30 at night.
