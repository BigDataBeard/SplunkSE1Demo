# SplunkSE1Demo
SE1 Certification Demo for Splunk
SE1 Demo Script
Cory Minton - 2016

#if you see something highlighted, it is probably a click or command entry.

Have browser opened to Splunk and click on the b-leaf demo app and have the lightbulb up

Setup a Scenario: 

Let’s say that you are Project Manager in the marketing department at MasterCard. In this case, MasterCard happens to already be a very good Splunk customer (and a good EMC customer running Splunk on EMC, but I digress), but the use cases for Splunk have been purely focused on IT Operations and a little bit of security, but definitely not really used in the lines of business. 

The untold story here is the CTO and CIO love Splunk and want help funding an upcoming expansion to their license to accommodate not only their use cases, but some additional ones that will make this purchase easier to justify with the CFO.  Because Splunk was a tool that started in IT, it represents a unique opportunity for the CIO and CTO to be more transformational to the business and garner support/funding previously help hostage by the EDW/BW teams.  The CIO and CTO are fostering these conversations, but it has been made to appear totally selfless and focused on the business value…not that there’s anything wrong with that.  I am playing the role of an EMC Splunk Ninja who has relationships outside of IT and has been asked to met with you to explore expanding use cases for Splunk at MasterCard. 

Begin Meeting: 

Hi Timothy, 

So this is a follow up to the meeting we had a few weeks back when I gave you that 30 minute talk on the big picture of why Splunk is so awesome.  If you recall, we talked a lot about: 
	•	how Splunk can make machine data usable and valuable to everyone
	•	how it can scale from your desktop to 1000s of machines
	•	how easy is it to get data into splunk and apply that universal index giving you rapid time to value
	•	and how it has become a true platform for enterprise analytics 
But that was just talk and today my hope is to put some meat on that bone and show show the basics of Splunk to get you comfortable with how some of the basic features of Splunk work, then jump right into a real life scenario I have crafted that I think will be very close to some of your current project objectives. 

And let’s try to keep this conversational.  I have some ideas of what I want to show you and some of what I show you may spur thoughts for you that I would be most happy to explore.  If you want me to explain something in more detail, just ask.  If you want me to move on, it’s cool…I did put on my big boy pants today.  So, feel free to interrupt me and help me make this a valuable time investment for you.  Cool? 

Alright, let’s get started. 

click on SPRAD

Let’s talk about what we are going to cover.  SPRAD stand for Search, Pivot, Report, Alert, Dashboard.  

Unpack each of those topically…just talk through the keys to SPRAD with the breakdown on screen

Click Search menu item.

Part of the beauty is natural language searching…it’s like google for all your data.  try something like: 

#enter search syntax 
fail* 

Notice all the field extractions and what machine data looks like when indexed. 

#Enter the search syntax 
index=”main” 

Splunk give you the opportunity to put all types of data into a single repository for simple search, which means you don;t have to go poking around to lots of different databases or repositories to find the data. 

Choose the Last 60 minutes in the time picker.

And you will find out very quickly that Splunk organizes data very neatly into time-series format, making it super simple to focus your efforts at finding meaningful insight in your data. 

Also notice the histogram that is populating here…this visualization helps our human eyes start to pick out patters that might lead to insights.  Again, half the battle for a lot of analytics projects is finding patterns, and no computer is as good as your brain at that, so we just try to power your intuition as fast as possible 

Then on the left, notice that Splunk has been smart enough to start to pull out interesting fields for the data we have begun to investigate.  Splunk does not know what all these fields are, it simply knows that with its schema on the fly process, these fields seemed interesting based on values and content.  Now, if we were looking for problems in a process, what works might we be looking for? 

Maybe errors?   

Click on "ERROR_MESSAGE"

Notice how we automagically got insights on the top 10 occurring types of error and are presented with options to do some statistical operations to the data we are currently searching, just by clicking the mouse, not by writing code?  Pretty cool, right? 

Now, you will notice that we are seeing a lot of events.  That is cool and all, but may not help us solve the problem we are after.  Sow what if we were to know that the issue we are trying to solve is really around minimizing errors in a customer online transaction so that we can improve transaction conversion?  So we talk with the IT team and we figure out that all the data we want is coming from our POS systems and the types of issues we are interested in are in the field “respCode” and their value is some number in the 200 range, which is system type errors…so we type: 

#Update the search syntax in search bar to:
index=”main” sourcetype=”pos:bus” respCode=”2*” 

Now, there is still a lot of events showing up here, so let's look at some ways to get more granular.  So far, we really haven't used any complex language for query, more human language type interactions and click of the mouse, but Splunk also allows users to interact with Search using an extensive, transformative language options for data analysis. 

Let's try making this data more visually pleasing with one of those transformations... 

#Update the search syntax to:
index=”main” sourcetype=”pos:bus” respCode=”2*” | timechart count by ERROR_MESSAGE
Select “visualization"
Then change to column chart and format to stacked
save as report to show how to make this repeatable
create a dashboard for tim with this as a panel

Pivots

In your role, you may or may not ever want to deal with data in this way.  Or maybe folks on your team may not want to.  Either way, Splunk gives you a powerful interaction method with your data that abstracts the search creation part of this process, allowing users to really focus on using the data.  It’s called Pivot.  A good way to think about this is that Pivot is to search what a spreadsheet is to a calculator.  Sure you can work out every problem with a little effort, but why not accelerate and automate the calculations and data manipulations so your work can scale?  Many times, business users want that point and click experience, so the goal of Pivot is to pre-arrange data into useful data collections and models that powers that desired end use experience. 

#Click Pivot menu item
#Click the Pivot Baseline with terms knowledge object

Notice the look and feel here.  Although search is still part of this tool, we don’t see it.  We see a graphical interface for building data transformations and visualizations.  No need to fool with messy, raw data, but rather we work with recipes designed around Data Models.  Again, the key here is immediate gratification with data. 

Choose the Last 60 minutes in the time picker

time series constant  
point and click 
instantaneous analysis 

So let’s continue with the error thread from earlier... 

click menu under Split Rows
select ERROR_MESSAGE

easy, instant gratification 

pick the Pie Chart from the visualization picker.

That’s what I like to call the quick pick of visualizations.  It gives the user great control and simple tools to build powerful data products in a short time. 

Reports

Now, we have shown two ways to interact with the data in a very flexible way, searching and pivoting out way to the answers we seek.  But not everyone wants to find the answers; rather there are folks out there who just need answers delivered to them.  When you want to automate the distribution of knowledge and collaboration, reports are there for you.  They take in all the search experience and proprietary knowledge that fuels your operations landscape, but simply pass it on…whether on demand, on a schedule, or via email. 

Think of it this way, reports simply recycle knowledge that is important to your group and automate the results…with no need for consumers of those reports to have any Splunk training.  This is how you share knowledge…and we know sharing is caring! 

Click on reports menu item.

The goal here with reports is to expose a broader audience to the data and visualizations you and your team have created that will be helpful in making decisions and driving the business objectives. 

Pick the Baseline report.

Each report is a knowledge object that holds certain information applicable to some scenario in your environment.  Users might all use this report as the baseline to build other reports, visualizations or dashboards. 

Click on reports menu item.
Pick the Baseline with terms report.

By adding additional terms, we have given this automated report a bit more granularity, specifically we are looking now at only events coming out of our POS systems.  Again, this may be handy for folks collaborating on specific business needs to give a consistent starting point and lens by which to view the data without all the clutter of too much data to analyze. 

Click on reports menu item.
Pick the Baseline with terms transformed into a time chart report.

As we have said before, the human eye and mind are great at patters, so maybe the best thing you can provide certain users is a consistent set of reports with visualizations.  We have reduced the noise of data not pertinent to our business need and have given users an interactive tool to analyze the data.  While we have abstracted the search work from view, it is absolutely still there, driving all we are doing.  Advanced users could use reports as the jump off point for more detailed analysis using advanced search capabilities, or they can just be a visualization for less technical users…or just about anything in between. 

So reports are again super useful for collaboration, automation, and distribution of knowledge you and your team are creating in Splunk. 


Alerts

The next thing we want to talk about is how we push data driven alerts into your operational processes, taking the knowledge you build in Splunk and allowing it to interact with workflows.  When a condition is found, like say an application server not accessible, then you want to do something about it.  Alerts allow you to build actions that layer in conditions across many parts of the enterprise and your technical assets.   

The highlights for alerts are event notification as a baseline, then the ability to integrate that into your business processes and automate your runback as much as possible. 

Click on the Alerts menu item.

talk about the organization being similar and consistent. 

Pick Alert Baseline for errors or failure alert

Results display shows the metadata about the alert and the results history, giving you the ability to look back into what triggered the alert. 

click on View Results to show how it was triggered.

Dashboard

Dashboards are really the culmination of labor in which you consolidate knowledge for collaboration.  A dashboard captures relevant KPIs, detailed analysis, and key transformational findings into interactive, collaborative, and prescriptive views that can be tailored for many use cases and stakeholder in your business.  Think of dashboards as the reason we’ve been searching, reporting, pivoting and alerting….it is the penultimate experience we can deliver back to a user.  Dashboards are like air traffic controllers…proving all the essential information necessarily to direct and maintain your operations.   

The main objective of these dashboards is to consolidate knowledge in a way that fosters collaboration and communication of critical information.  

Click Dashboard menu item.
Click SPRAD sample dashboard

In this dashboard, we are showing simple the visualization of the work we’ve done over the last few minutes.  Abstracting complexity away and simply presenting information visually.  Breaking down cultural barriers through visual queues we all understand. 

While the complexity is abstracted, we have not lost the interactive nature of the knowledge objects we’ve built.  Simply by hovering over any area, we can drill into the information and are offered unique abilities to leverage this knowledge further.   

Ok, so you have a good view of the underlying tools that make up much of what Splunk enterprise is really all about.  Any questions before I move on to a real life scenario I think you will find very relevant? 





Scene Demo

Click leaf app at top menu.
Return to main light bulb screen.
click scene.

Click through.

Imagine you are a payment services provider. In your line of business you offer a variety of services such as pre-paid cards, online payment solutions and physical point-of-sale terminal devices. 

lick through.

You are responsible for a new pre-paid card promotion. You have thirty days to achieve 30% market penetration. That means two thousand new subscribrers. The business objective in the first three months is to retain 50% of new subscribers and average about $1.2M in transactions per hour . 

Click through.

In order to keep track of the progress in the new promotion, you will monitor electronic service requests from multiple access points through the the banking network; specifically, you are focused on specialized Web services and the physical point-of-sales devices. 

Click through.

Splunk will acquire your data easily and quickly. Our Universal Machine Data Platform is open and extensible; it delivers integrated, end-to-end data collection, management and analysis which helps amplify visibility across your entire environment. 

Click “Continue to next tour"

Again, the objectives here are: 
	•	in the first 30 days enlist 2000 new customers with a 30% engagement rate.
	•	in the first 90 days, retain 50% of new customers and average about $1.2M in transactions per hour.

To achieve our objectives, we want to insure that our systems operate smoothly and any error in the system can be removed to streamline the customer experience.   

For the rest, I defaulted to the page 26 and beyond of the micro scripts. 
