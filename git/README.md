<h1 style="color: #63d297">How to write Git commit messages</h1>

> **Note:** This has been all said before

We have our own rules of writing Git commit messages. The template of it is:

```
$ git commit -m "#<number-of-the-issue> - <front/back/devops> (Feature/Fix/Docs/Style/Refactor/Test/Chore/Grammar): <subject-of-the-commit>"
```
Here:  
`number-of-the-issue` - is the number of the issue that Gitlab gave to it, when it was created.
While we use Gitlab, this number is the mandatory.  
`frontend/backend` - it is description for which part of the project commit is related.  
In parentheses there are types of the commit:  
`Feature` - new feature for the user, not a new feature for build script.  
`Fix` - bug fix for the user, not a fix to a build script.  
`Docs` - Changes to the documentation.  
`Style` - Formatting, missing semicolons, etc; no production code change.  
`Refactor` - Refactoring production code, e.g. renaming variable.  
`Test` - Adding missing tests, refactoring tests; no production code change.  
`Chore` - updating grunt tasks, deleting commented code, etc.; no production code change.  

Your Git commit message could contain only the subject, or the subject and the body. Let's talk about that.

> **Note**: Examples that you'll see below are not written using our patter for simplicity.  
> If you see example like `$ git commit -m "Do something useful in this commit"`,  
> then you should understand that in the project we use:  
> `$ git commit -m "#<number-of-the-issue> - <fronted/backend> (<type-of-changes>): do something useful in this commit"`

There are seven rules that will make your Git messages better:  

1. [Separate subject from the body with the blank line](#1-separate-subject-from-the-body-with-the-blank-line)  
2. [Limit the subject line to 50 characters](#2-limit-the-subject-line-to-50-characters)  
3. [Don't capitalize the subject line](#3-dont-capitalize-the-subject-line)  
4. [Do not end the subject line with a period](#4-do-not-end-the-subject-line-with-a-period)  
5. [Use the imperative mood in the subject line](#5-use-the-imperative-mood-in-the-subject-line)  
6. [Wrap the body at 72 characters](#6-wrap-the-body-at-72-characters)  
7. [Use the body to explain *what* and *why* vs. *how*](#7-use-the-body-to-explain-what-and-why-vs-how)

Also you'll find methods [how to write body in Git commit message](#how-to-write-body)

But first let's look at real good Git commit message below.

![img.png](good-git-message.png 'The good Git commit message')]

## 1. Separate subject from the body with the blank line

Why do we need a subject? **Subject** is needed for short lookup of what have been
done in the commit. Subject is the first sentence in your commit message, and it must
show the big picture of the commit. In the **body** you could write details about what 
and why was changed/added/removed (use the [7th rule here](#7-use-the-body-to-explain-what-and-why-vs-how)). But you
should know that not all commit messages needs the body, some commits are good to go 
with only the subject.

If your commit don't need the body, just use ``git commit -m <message>``:

```git commit -m "Fix typo in 'My advertisements' page"```

The example above don't need the body as there cannot be any 'useful' details.
What would you write there: ``"Changed type in word 'advirtisements', and now it
is 'advertisements'"``? It's useless, cause your colleague could see this fix in
diff section in the IDE.

If we fixed function ``fetchData()``, that were fetching data twice from
the backend, here how would look **great Git commit message**:

```
Fix function that were twice fetching same data

Function fetchData() had an if-statement that were implemented not
in the right way, so it were fetching data twice, as it fits both
of the conditions. Changed condition, and the function bothers
backend only once it's called.
```

How could we write that kind of Git commit messages? Of course, IDEs
are now allows you to do it with their interface, but we are looking 
for solutions in terminal. You better ~~watch yourself~~ use terminal,
cause knowing terminal commands is +some-amount-of-points on interviews.

### [How to write body](#how-to-write-body)

So, there are several ways to set your workspace that you can write body
for Git commit message. One of those is don't close the quotes when writing
the message. For example, I'm using JetBrains WebStorm on Mac OS, and this
works for me:

```
$ git commit -m "Writing here your commit's subject <Press 'Enter' here>
<blank line to divide subject and body> <'Enter' here to start writing body>
Write here your body, where you discribe what and why you did in details"
```
I checked it on Windows in its command line, and I've got an error
'Wrong commit message' or something like that. But you can try it on your own.

Also you can set your editor of choice as default Git commit message editor.
It's written [here](https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration)
If to be short, you can do it like this:
```
$ git config --global core.editor "code --wait" // VS Code
$ git config --global core.editor emacs // Emacs
$ git config --global core.editor vim // Vim
```

> **Note**: If you set ``--global`` attribute, it will change your Git commit
> message editor in all repositories. If you would like to change it in only one
> repository (where you are writing this command), write ``--local`` instead.

Here is a thing with Vim - you don't need to make it default editor, because
you can open editing Git message with ``git commit -a``. This command will open
editing commit message in Vim without defining it as default editor.

> **Note**: As we use numbers of issues in git message 
> (e.g. for issue #80 it will be 
> ``git commit -m "#80 - frontend (Feature): <message here>"``). As Git use the
> ``#`` as comment definition character, what we've written above will disappear in
> the result. To solve this problem we have to change comment character in git config,
> what we could do just with the ``git config --global core.commentChar <your
> character here>``.

On that note first rule is over :).

## 2. Limit the subject line to 50 characters

It's as easy as it sounds - don't let your subject be more than 50 characters.
The point is that the subject should have only **main** change of the commit.
If you think that you can't describe all your changes in 50 characters, well,
then you did not that good job, because commits should be more 'atomic' - they
must change not the whole component, for example, but some part of it. In that
case, if you did a lot of changes, and now you need to commit them, you can
``git add <file name>`` and commit each file or several files describing in commit
message changes made in them. That solves the problem.

## 3. Don't capitalize the subject line

<strike>Another simple rule. As subjects are 'titles' of our commits, like titles of
books, movies or anything else, they should start from upper case letter.
It's not an obligation, but agreement in the <span style="color: #63d297">
**Staq Dev Studio**</span>. If you are not agree with that, explain your
  position, and our style guides could be changed.</strike>
  
New: We don't do that here anymore, ha))) (c) Lema

## 4. Do not end the subject line with a period

At least it looks not cool. As every subject (read as 'commit') is not associated
with another subject, we don't need period between them. For example:
```
5f08bd34 #80 - frontend (Feature): create Delayed posts page with same named component
409879fa #69 - frontend (Chore): resolve warnings and deleting unused code
669fbc7b #73 - frontend (Fix): fix wriggling in exchange page
727dab41 #74 - frontend (Fix): change the way statistics filter behave on mobile screens
```

Now let's look at example above, but with periods:
```
5f08bd34 #80 - frontend (Feature): create Delayed posts page with same named component.
409879fa #69 - frontend (Chore): resolve warnings and deleting unused code.
669fbc7b #73 - frontend (Fix): fix wriggling in exchange page.
727dab41 #74 - frontend (Fix): change the way statistics filter behave on mobile screens.
```
Meh.

Just don't use period, it's also agreement.

## 5. Use the imperative mood in the subject line

*Imperative mood* just means “spoken or written as if giving a command or 
instruction”. For example:

- Clean the table
- Close the window
- Take out the trash

Even Git uses imperative mood in it's commands:

```
Merge branch 'myBranch'
Revert 'Change the thing with something'
```

So, when we write Git commit message's subject we have to write in imperative mood:

- Create Delayed posts page with same named component
- Resolve warnings and deleting unused code 
- Fix wriggling in exchange page
- Change the way statistics filter behave on mobile screens

not 

- ~~Created Delayed posts page with same named component~~  
- ~~Resolved warnings and deleting unused code~~  
- ~~Fixed wriggling in exchange page~~  
- ~~Changed the way statistics filter behave on mobile screens~~

A properly formed Git commit subject line should always be able 
to complete the following sentence:

- If applied, this commit will ***your subject line here***

In above example it will be:
- If applied, this commit will ***create Delayed posts page with same named component***
- If applied, this commit will ***resolve warnings and deleting unused code***
- If applied, this commit will ***fix wriggling in exchange page***
- If applied, this commit will ***change the way statistics filter behave on mobile screens***

## 6. Wrap the body at 72 characters

When you are writing Git commit message body, it's lines should not be more
than 72 characters. Not sentence, but line. We have an agreement that allows us
to write body lines with formula **length-of-the-subject-line (what we expect is 50 characters
long) + few words**.

```
First second third fourth fifth sixth seventh word

First second third fourth fifth sixth seventh eighth ninth tenth word!!!
```

In the example above we have the subject, that is 50 characters long, and body line,
that is 72 characters long. As you see, body line is a few words longer that the
subject line.

## 7. Use the body to explain *what* and *why* vs. *how*

Body in commit message uses to describe ***what*** problem were in the changed file
and ***why*** the problem occurred.

> **Note** that **what and why** are not the only questions, and they are not the only ones.
> In development may happen anything, and that means questions above could be not
> enough to answer. Just be sure, that you don't explain **how** you solved the problem,
> because the answer to **"How?"** is the diff section of the IDE, Github, Gitlab
> and etc.

For general growth I suggest you to read real Git commit from 
[Bitcoin Core](https://github.com/bitcoin/bitcoin/commit/eb0b56b19017ab5c16c745e6da39c53126924ed6), 
where all the rules above are followed.
---
**(07.06.2021) UPD**: Zelim Gerikhanov, Said-Magomed Sadulaev, Abdul-Malik Abubakirov, Lom-Ali Gurzhikhanov
and Aslambek Abubakarov voted for writing commit message title by lowercase letter, i.e.
`#<number-of-issue> - <front/back> (<type>): some title of the commit starting from the lowercase letter`.

---
[Shamil Khashaev](https://github.com/skhashaev)
