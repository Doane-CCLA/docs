# Using Jetstream Virtual Machines in your Allocation
### If you need to know how to login to Jetstream through the Atmosphere Graphical User Interface, please see the preceding section: [Accessing Atmosphere on Jetstream](accessing-atmosphere-on-jetstream.md)

<br>

1. First we will need to log in to https://use.jetstream-cloud.org and navigate to the "Images" page.   
![View of the Jetstream Virtual Machine Images Page](./screenshots/jetstream-vm-images-page.png "View of the Jetstream Virtual Machine Images page")

2. For this example, we will search for an image with Anaconda 3 installed. Type "anaconda" into the search bar as shown below. Jetstream has a "live" search bar so it will start filtering the VM images as soon as you start typing.   
![Typing in our search term of anaconda](./screenshots/vm-search-anaconda.png "Searching for a VM with the word anaconda")

3. If we scroll down the page we will see an image titled "Doane CST210 Ubuntu". This VM image looks like it has everything we need.   
![Scrolling down to find the Doane CST210 Ubuntu VM Image](./screenshots/finding-doane-cst210-vm.png "Scrolling down to find the Doane CST210 Ubuntu VM Image")

4. While we are here, I am going to favorite this VM image by clicking the star in the upper right corner of the VM's panel as shown below. The star should now be filled in with a color.   
![Clicking the star to favorite this VM image](./screenshots/favorite-the-doane-vm.png "Clicking the star to favorite this VM image")

5. Now, we will scroll to the top of the page and click on the "FAVORITES" button in the VM Images Navigation Menu. This way we can have fewer VM images filling up our screen.   
![Clicking on the FAVORITES VM navigation menu button](./screenshots/navigate-to-vm-favorites.png "Click on the FAVORITES VM navigation menu button")

6. Once there, we will now click on the "Doane CST210 Ubuntu" VM image panel. Clicking anywhere in the white area of the panel will work.   
![Clicking on the Doane VM panel](./screenshots/nav-to-fav-doane-vm.png "Click on the white area of the Doane VM image panel")

7. This new page provides detailed information about the selected VM image. This includes previous versions of the VM image and what was changed in each version.   
![Details of the Doane CST210 Ubuntu VM image](./screenshots/doane-vm-details.png "Details of the Doane CST210 Ubuntu VM image")

8. If you are happy with the information provided and think this VM will work for your needs, we will need to create a project to actually store and run the VMs related to our project. In the top (main) navigation menu, click on the "Projects" button.   
![Clicking on the top navigation menu Projects button](./screenshots/nav-to-projects.png "Click on the top navigation menu Projects button")

9. Once on the projects page, click on the "CREATE NEW PROJECT" button as shown below.   
![Clicking on the CREATE NEW PROJECT button](./screenshots/create-new-project-1.png "Click on the CREATE NEW PROJECT button")

10. Now enter a name and description for your new project. Click the "CREATE" button when you are finished.   
![Filling information and clicking CREATE](./screenshots/create-new-project-2.png "Fill out the information and click CREATE")

11. Now we have successfully created a new project.   
![View of our new project](./screenshots/create-new-project-3.png "View of our new project")

12. Click on the Project panel to open up the detail page for the project.   
![View of the details page for our new project](./screenshots/new-instance-1.png "View of the details page for our new project")

13. From here we will want to click the pink "NEW" button which will open a drop down menu. In the drop down menu select "Instance" to begin the process of making a Virtual Machine.   
![Click the NEW button and select Instance from the drop down menu](./screenshots/new-instance-2.png "Click the NEW button and select Instance from the drop down menu")

14. Once the new popup page opens, click on the "Show Favorites" tab to bring up our favorited VM images.   
![Clicking Show Favorites in the new Instance popup page](./screenshots/new-instance-3.png "Click the Show Favorites in the new Instance popup page")

15. Select you desired VM Image you want to use for your new Virtual Machine. After doing that, you will be brought to the next step in the Instance Wizard. Here you can specify the information for the VM. These options include the Instance Name, version of the Base Image to use, the Project that the VM she be housed in, which allocation account that Jetstream should charge for the VM, and the physical Size for the VM. Jetstream also provides a graphical representation of how much of the allocation resources this instance will use given the selected configuration.   
![Customization options for the new VM instance](./screenshots/new-instance-4.png "Customization options for the new VM instance")

16. We will cover the advanced options in another tutorial. For now, when you are happy with your configuration options, click the "LAUNCH INSTANCE" button. This and the next few steps to launch the VM will take around 25 minutes to complete.   
![Clicking the LAUNCH INSTANCE button to start the new VM](./screenshots/new-instance-5.png "Click the LAUNCH INSTANCE button to start the new VM")

17. Once it is done loading, the VM will be added to the queue to be built and will have a Activity status of "Scheduling".   
![View of the deployment status for our new VM instance](./screenshots/new-instance-6.png "View of the deployment status for our new VM instance.")

18. Once the VM is successfully built, it will move to the Activity status of "Initalizing".   
![Updated view of the deployment status for our VM instance](./screenshots/new-instance-7.png "Updated view of the deployment status for our new VM instance")

19. When the VM is done being built, scheduled, and deployed, the status will turn from a yellow dot, to a green dot. A note of warning, now that the VM is active, it WILL be charging the allocation account. Please make sure to shelve your instance once you are done with it to quit being charged for the resources.

20. To shelve or "turn off" your VM.
