# Testing Protocol (with appendices)

This is an attempt to outline the various ways in which we can test out web applications. Certain web application concepts are mentioned multiple times and include links to relevant appendices that explain them in more detail.

**Automated testing: (limited verification still required)**

Basic Object Functionality

1. CRUD
    1. Can I create this object?
    2. Can I read or view this object?
    3. Can I update or edit this object?
    4. Can I delete this object?
2. Relationships
    1. When I **create** this object, are the **applicable related objects created** with it?
        1. What related systems does this action trigger? Are the **applicable related systems triggered** properly?
    2. When I **view** this object, are the **applicable related objects shown** with it?
        1. What related systems does this action trigger? Are the **applicable related systems triggered** properly?
    3. When I **update** this object, are the **applicable related objects updated** with it?
        1. What related systems does this action trigger? Are the **applicable related systems triggered** properly?
    4. When I **delete** this object, are the **applicable related objects deleted** with it?
        1. What related systems does this action trigger? Are the **applicable related systems triggered** properly?
3. Permissions
    1. As a &lt;xyz> user, can I **create** this object?
    2. As a &lt;xyz> user, can I **view** this object?
    3. As a &lt;xyz> user, can I **update** this object?
    4. As a &lt;xyz> user, can I **delete** this object?

**Manual testing:**

Usability

1. [Forms](#Forms)
    1. When I submit the form, am I given a clear indication that the form is being processed?
    2. Can I submit the form **with** the required fields? Can I submit the form with **all fields**? Does the request succeed, and am I given a clear indication that it has?
    3. Can I submit the form **without** the required fields? If I try to, am I prevented from doing so and given clear, appropriate, and actionable error message(s)?
        1. If I fix the errors and resubmit, does the request succeed, and am I given a clear indication that it has?
    4. Does the form clearly indicate its fields, the purpose of each field, and the type of data it expects?
    5. Can I submit the form **with erroneous values** in the fields? If I try to, am I prevented from doing so and given clear, appropriate, and actionable error message(s)?
        1. If I fix the errors and resubmit, does the request succeed, and am I given a clear indication that it has?
    6. Considerations for file and image fields
        1. Is there a max upload size limit? What happens when I try to upload a file that’s too big?
        2. Are there restrictions on file extensions? What happens when I try to upload a file with a different extension?
        3. If this is an image field, what happens when I try to upload a non-image file?
    7. [Edge cases](#How-requests-work)
        1. After I successfully submit the form, what happens if I click Back on my browser and submit the form again?
        2. What happens if my internet connection cuts out before or while I’m submitting the form?
        3. What happens if my [session](#Sessions-Cookies-and-the-Stateless-Nature-of-HTTP) expires and I submit the form?
        4. What happens if I click the Submit button many times in quick succession?
        5. Say I have two tabs open with the same form, Tab A and Tab B. I’m filling out the form in Tab A and switch to B. [I log out of the app](#Sessions-Cookies-and-the-Stateless-Nature-of-HTTP) in Tab B. Later, I’m back on Tab A, forgetting that I’ve actually logged out. Now I submit the form in Tab A. What happens?
2. [Modals](#modals)
    1. Is there some sort of title on the modal? If so, does it alert me to the content within?
    2. Does the content of the modal clearly convey an alert, warning, error, or piece of information that I can act on?
    3. Can I close the modal? If there is no close button, is there a button that lets me acknowledge the content and subsequently close the modal?
    4. If the modal poses a question, can I answer “yes” or “no”? If the modal confirms an action, can I confirm the action or cancel the action?
    5. Should the modal close when you click outside of it or hit ESC? Can I signal my acknowledgement of the content by hitting ENTER?
    6. Edge cases
        1. What happens if I click the confirmation button many times in quick succession. Is the action triggered more than once?
        2. What happens if my internet connection cuts out before or while I’m clicking the confirmation button?
3. List Pages
    1. How does the list page account for multiple records? One record? No records? Does the language and design on the page change to match each case?
    2. Can I sort the records? Can I search or filter them by one or more parameters?
    3. Can I save or replicate my search later?
    4. [Edge cases](#How-requests-work)
        1. What happens if I click on a record that gets deleted before or while I click on the record?
        2. What happens if I click on a record and I’m blocked from viewing the record before or while I click on the record?
4. Single Record Pages
    1. See Basic Object Functionality
    2. Edge Cases:
        1. See Edge Cases for List Pages
        2. If me and another person are accessing the same page, [what happens if we submit our changes at or near the same time?](#How-requests-work)


## Appendices 

### Forms

A form is a component of web pages that allows a user to insert, attach, or fill out information within form fields and submit it to the server for processing.

Form fields expect a certain type of data. This is normally inferred by the label of the field, the type of HTML element used, and any help text included. Further inspection of the HTML element itself can also reveal the type of data it expects (e.g. for an `<input>` element, the `type` parameter can be “text”, “date”, “password”, “file”, and more).


    Each field should have a label. If it does not, it should have some other visual means of distinguishing the field. If there is no text at all associated with the field, it should include an “invisible” label for screen readers.

For example, let’s take a checkbox-type field called Verbosity. Normally, the field should display a label of “Verbosity” with a checkbox somewhere nearby. If we wanted to be a bit clearer on the purpose of this field, we may omit the “Verbosity” label and instead write something like “Send notifications for all activity to each assigned user”. This still communicates the purpose of the field.

An example of a field with no label or text might be a captcha. These are normally embedded “tests” for users to prove they are human. The embedded test will contain some text like “I’m not a robot”. That may not be clear for someone navigating the page with a screen reader. Thus, we should include an “invisible” label for the field (like “Captcha”) so that the user knows this is a captcha.

**Accessibility**

There are multiple ways to increase accessibility in forms, and this section is by no means exhaustive. Our browsers will add some accessibility features but we need to include more.

Aria: [https://www.lullabot.com/articles/what-heck-aria-beginners-guide-aria-accessibility#](https://www.lullabot.com/articles/what-heck-aria-beginners-guide-aria-accessibility#)

“Invisible” labels: [https://getbootstrap.com/docs/4.5/utilities/screen-readers/](https://getbootstrap.com/docs/4.5/utilities/screen-readers/)

`alt` and `title` tags: [https://www.w3schools.com/tags/att_alt.asp](https://www.w3schools.com/tags/att_alt.asp) | [https://www.w3schools.com/tags/att_title.asp](https://www.w3schools.com/tags/att_title.asp)


### Modals

A modal is a component of modern web pages that conveys an alert, warning, error, piece of information, question, or a confirmation of an action. It takes the form of a dialog box and pops up on top of the web page, usually blurring and/or darkening the rest of the web page. The user can, at the very least, close the modal, either by clicking an X button at the top right of the modal or clicking a button inside the modal that signifies an acknowledgement of the content or a dismissal.

For modals that pose a question or confirm an action, there are usually two buttons. One, usually on the left, is for dismissing the modal, rejecting the action, or saying “no” to the posed question. The button on the right is for confirming the action or saying “yes” to a question. Clicking this button usually closes the modal **and** triggers an action on the web page.

Default behavior also includes closing the modal when clicking outside of it or pressing the ESC key.

**Accessibility**

Same as forms. Buttons and their actions should be clarified for screen readers.


### How Requests Work

When you type a URL into the address bar of your browser, click a link/button on a web page, or submit a form on a web page, you initiate a **request**. You are requesting the server to give you a web page and passing additional information with your request for the server to process.

Your request follows a multi-step path to the server, from your computer to your ISP, to a DNS server, through a VPC, and finally to the server itself. The server then runs code for the URL that you requested, passing in any additional information you sent along (cookies, headers, GET or POST variables, body), and returns a **response**, usually consisting of a bit of information and a static page in the form of HTML. Your browser receives this HTML and renders it into the web page you finally see.

Standard requests on a website are normally synchronous, meaning your browser waits for a response before displaying new information. However, websites, and objects on those websites are accessible by anyone at any time. This means that you and another person can both, say, view settings for a Group (if you both have access) **at the same time**.

**Issues arising from requests**

Let’s continue the example above to discuss a common problem with web applications. Let’s say person A and person B both access the settings page for a Group at the same time. Person A writes in a **new title** for the group. Person B writes in a **new description**. Person A submits their change. Moments later, Person B submits their change. What does the Group look like now?

This is an example of a **race condition**. Both Person A and B submitted changes to the same object at nearly the same time. Using the example above, the Group will first be saved with A’s new title. Moments later, the Group will be saved again, with B’s new description **but also the old Group title**. Person B has overwritten Person A’s changes.

Race conditions can be solved in multiple ways. One is to use a **transaction**, or a “lock”, on the object. Person B cannot edit the Group until Person A is done with their changes. This can be implemented on the front-end, with some kind of locking mechanism where Person A “locks” the group while they’re editing and Person B cannot access the edit page until Person A submits changes or leaves the page. We can also use a database transaction. Database transactions are useful for simultaneous changes. If Person A and B happened to submit changes **at or near the same time**, whoever is first will lock the Group from other changes. So, when Person B submits changes at or near the same time, the database rejects them, whereby the system either communicates the failure to Person B or simply waits for the lock to be removed and the proceeds with the changes.

Another way is to only allow editing of fields individually. That way, worst case-scenario, the race condition happens for a single field, and the data loss is minimal (or non-existent if you used a transaction). We can also use a similar method where we only update fields that have new values. This way, in the example above, when the race condition happens, Person A gets their new title saved and Person B gets their new description saved. Though the issue arises again if both people make changes to the same field.


### Sessions, Cookies, and the Stateless Nature of HTTP

Web pages are traditionally served to us using a protocol called Hypertext Transfer Protocol, or HTTP. This protocol is stateless, meaning that no data is saved or retained between requests; there is no way to discern one request from another. This problem is solved using two technologies: **cookies** and **sessions**.

With a **session**, information relevant to a specific set of requests (in this case, requests made by the same user) is stored on the server. A unique id is then stored in the user’s browser. This id is sent with every request the user makes, and thus the server is able to tell two things: the request came from a specific user, and any relevant information for this user (the session) should be grabbed and applied to the request.

A **session** is started by a user logging in to a website. A session is usually persisted for a finite amount of time that varies by website. Sometimes, it’s a day. Sometimes it’s thirty days. When the time is up, the session “expires”; the user must log in again to start a new session. A session can also be “expired” manually by the user logging out of the website.

Remember that a user’s session id is stored by their browser? This takes the form of a **cookie**. A cookie is a piece of information stored by a user’s browser that is sent to the server, attached to your request, every time you make a request.
