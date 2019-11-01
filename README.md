# Live Project

## Introduction

During my time at The Tech Academy, I worked with my peers in a team on a MVC Web Application in C#/ASP.Net. This project was a great opportunity to learn what it was like to have multiple people working on one project and improve the product. Most of the website was already built, so there was no time wasted on creating the website from scratch, and I got to experience what it was like to dive into a project that had already been started and to assimilate myself with the code that had already been written. I worked on several [front end stories](#front-end-stories) and [back end stories](#back-end-stories) to improve the look and functionality of the website. Over the two week sprint, I also had the opportunity to participate in daily meetings and weekly sprint retrospectives which offered insight into project management [skills](#other-skills-learned). I am confident I will be able to utilize these skills in any future project.

## Front End Stories

* [Redesigned Login Page](#redesigned-login-page)
* [Background Image Stretching](#background-image-stretching)


### Redesigned Login Page
The login page had a username and password text field, as well as a few buttons for login convenience. Everything was lined up vertically on the left side of the screen. I was tasked with moving the login buttons to the center of the screen and placing them side by side as well as adding three new buttons to login with social media accounts. This was accomplished with both editing the CSHTML page and the CSS elements.
  

````
   <div align="center">
      <div class="row justify-content-center">
          <div class="loginItemContainer col-md-6">
              @Html.CheckBoxFor(m => m.RememberMe)
              @Html.LabelFor(m => m.RememberMe)
          </div>
          <div class="form-group loginItemContainer col-md-6">
              <input type="submit" value="Log in" class="btn loginItemBtn darkbluetext" />
          </div>
      </div>
      <div class="row justify-content-center">
          <div class="loginItemContainer col-md-6">
              @Html.ActionLink("Register as a new user", "NewUser", "Account", null, new { @class = "loginItemAnchor" })
          </div>
          <div class="loginItemContainer col-md-6">
              @Html.ActionLink("Forgot your password?", "ForgotPassword", null, new { @class = "loginItemAnchor" })
          </div>
      </div>
      <div class="form-group">
          <div class="loginItemContainer col-md-6">
              @Html.ActionLink("Back", null, null, new { Href = Request.UrlReferrer, @class = "loginItemAnchor" })
          </div>
      </div>
      <div class="row justify-content-center">
          <div class="col-md fbItemContainer">
              <input type="submit" value="Login with Facebook" class="btn loginItemBtn" />
          </div>
          <div class="col-md twitterItemContainer">
              <input type="submit" value="Login with Twitter" class="btn loginItemBtn" />
          </div>
          <div class="col-md googleItemContainer"> 
              <input type="submit" value="Login with Google+" class="btn loginItemBtn" />
          </div>
      </div>
  </div>
 ```` 
  
The CSS for the buttons also had to be updated.

````
.fbItemContainer {
    background-image: linear-gradient(to right, #659EC7 0%, rgba(93,172,244,1) 51%, #0000CD 100%);
    color: white;
    margin: 15px;
    padding: 0px 15px;
    box-shadow: 0 0 20px #9681c1; /*#a38fcc;*/
    max-width: 190px;
    width: 100%;
    line-height: 38px;
    border-radius: 5px;
    height: 38px;
    line-height: 38px;
    text-align: center;
    transition: 0.5s;
    flex: 1 1 auto;
    background-size: 200% auto;
}
    .fbItemContainer:hover {
        background-position: right center; /* change the direction of the change here */
    }

.twitterItemContainer {
    background-image: linear-gradient(to right, #659EC7 0%, rgba(93,172,244,1) 51%, #0000CD 100%);
    color: white;
    margin: 15px;
    padding: 0px 15px;
    box-shadow: 0 0 20px #9681c1; /*#a38fcc;*/
    max-width: 190px;
    width: 100%;
    line-height: 38px;
    border-radius: 5px;
    height: 38px;
    line-height: 38px;
    text-align: center;
    transition: 0.5s;
    flex: 1 1 auto;
    background-size: 200% auto;
}
    .twitterItemContainer:hover {
        background-position: right center; /* change the direction of the change here */
    }

.googleItemContainer {
    background-image: linear-gradient(to right, #659EC7 0%, rgba(93,172,244,1) 51%, #0000CD 100%);
    color: white;
    margin: 15px;
    padding: 0px 15px;
    box-shadow: 0 0 20px #9681c1; /*#a38fcc;*/
    max-width: 190px;
    width: 100%;
    line-height: 38px;
    border-radius: 5px;
    height: 38px;
    line-height: 38px;
    text-align: center;
    transition: 0.5s;
    flex: 1 1 auto;
    background-size: 200% auto;
}
    .googleItemContainer:hover {
        background-position: right center; /* change the direction of the change here */
    }\
 ````
 
### Background Image Stretching
I was tasked with fixing an issue with the background image stretching on some pages and the whole image being viewable in other pages. After some research, I realized the issue was in the CSS coding, where the image would stretch to fit the size of the container. In pages that had more content, the image would stretch so that it would store all the content inside the stretched image. In smaller pages, the entire image would be viewable.

````
#site-header {
    background-image: url(images/bgimage.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: right;
    width: auto;
    height: 120px;
   
}
````

## Back End Stories

* [Drop Down List Database](drop-down-list-database)

### Drop Down List Populated From Database

This story was both Front and Back End, but the majority of it was back end. I added a drop down list to a Job Action page, with the contents of the Drop Down list populated from Jobs in our database. The goal was to be able to select a Job to attach the Job Action to, whereas before the Job Action would be automatically applied to which Job page it was opened on. This way, Job Action could be a standalone page later on. 

The front end part was relatively simple by adding a drop down. However, getting the list to grab the data from Jobs database was the challenging part.
````
<div class="form-group">
      @Html.LabelFor(model => model.Job, htmlAttributes: new { @class = "control-label col-md-2" })
      <div class="col-md-10">
          @Html.DropDownList("JobSelector", (IEnumerable<SelectListItem>)ViewData["Jobs"], new { @class = "form-control" })
          @Html.ValidationMessageFor(model => model.Job, "", new { @class = "text-danger" })
      </div>
  </div>
````
After implementing the front end for the drop down list, I had to go to the controller and add the logic for data to be pulled from the database and returned to the view.
````
 private void PopulateJobActionDropDowns(object model, int JobId = 1)
    {
        var jobSites = new SelectList(db.Jobs.ToList(), "JobIb", "JobTitle", JobId);
        ViewData["Jobs"] = jobSites;

    }
````
I've set the intial Job shown on the dropdown to be the first job in the list. That way, in the following Create action, it will always be populated by the integer that correlates to the job.
````
    // GET: JobAction/Create
    public ActionResult Create(int? jobIDJobFK)
    {
        var jobAction = new JobAction();
        PopulateJobActionDropDowns(jobAction);

        return View();
    }
    // POST: JobAction/Create
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create(int? jobIDJobFK, [Bind(Include =              "Job,JobActionId,Type,Name,Description,OrderedDate,DeliveryDate,StartDateTime,EndDateTime,URL")] JobAction jobAction)
    {
        PopulateJobActionDropDowns(jobAction);
        var JobId = Request.Form["JobSelector"].ToString();

          if (ModelState.IsValid)
        {
            jobAction.Job = db.Jobs.Find(Int32.Parse(JobId));

            db.JobActions.Add(jobAction);
            db.SaveChanges();
            return RedirectToAction("index");
        }
        return View(jobAction);
    }
````

## Other Skills Learned
* Using Microsoft DevOps to coordinate with a group of developers to improve an application.
