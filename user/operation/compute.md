---
layout: user-doc
title: Compute Nodes in Operation
---

The [compute component](../design/compute-component.html) tralalalalala



## Find Compute by IP

To find a VM IP address, follow these steps:

1. Click **Operate.**
2. Select the environment.
3. Select the platform.
4. Select the compute component from the list.
5. Select each compute to see the configuration tab and look for the public IP field.


## Fix Unresponsive Compute

To fix an unresponsive compute, follow these steps to reboot the compute:


1. Issues a reboot action from the operations of the compute component.
  
    ![Reboot Compute](/assets/docs/local/images/reboot-compute.png)
  
2. If the compute does not respond after the reboot, replace the compute. For instructions on how to replace a compute, go to <a href="/user/operation/replace-a-bad-vm.html">Replace a Bad VM</a>.
3. If it is not an option to replace the compute, contact your OneOps administrator for further assistance to bring the node up. 


## Use Operations for VM Tasks

Use Operations for most of the tasks you need to perform on a VM.

* Create an additional user in the design other than the app for the development team
* View realized instances for your platforms
* View graphs for monitors on defined metrics and thresholds
* Perform single or bulk operations like restart/ start/ stop on Tomcats


## Replace a Bad VM

Replacing a VM results in the loss of any data available with that VM, for example, log files etc. If you are replacing the VM for a Database or Cache, check with the respective teams before replacing the compute. Additionally, the IP address will change.

Below are the instructions to replace any VM instance when you need to. An example of when you might need to replace a bad VM would be if your team concludes that the failed VM instance cannot be restored for long time or ever. Replacements will generate new IP addresses so any time you do this you need to make sure the Nagios monitoring is adjusted.


1. Make sure that there is no active or pending deployment for the environment.
2. Go to Operations and then to the compute instance that is unhealthy and needs to be replaced. 
3. Select the **configuration** tab and click **Replace.** (Note that this only marks the VM for replacement in OneOps. It does not initiate the actual replacement immediately.)
4. To replace multiple VMs at a time, repeat steps 2 and 3 for any VM you need to replace. Also, you can do step 5 and perform the replacements for some of them before doing others.
  
    **Bulk Replace:** As an alternative to repeating steps 2, 3, and 4, for every instance to be replaced, a multi-select bulk replace operation is available in the component (instance list). Any instance that is already marked for replacement has a purple marker. To do a replace for additional instances, multi-select the instances and then select **replace** from the top-right list menu. The process is exactly the same as selecting individual instances to be replaced. This step only marks/prepares the instances for replacements. The actual replacement is done with the steps below.
  
5. To generate a deployment plan with the replacements steps, go to Operations to the top of the environment summary page and click **Force Deploy.** (Items in the plan have the left green arrow icon in the deployment overlay.)
6. Deploy.

>There is also an “Unreplace” button to unmark the VM should you change your mind before step (6). Once the deployment is kicked off, then it has to be completed.
Obviously the success of the replacement depends on the state of the OpenStack cloud. If there is a bad hypervisor, the Elastic Cloud team needs to ensure that it is disabled so that any new VM replacements do not get allocated to it and fail.





## Update the Size of a Compute

At this time, you can not update the size (Instance Types) of a compute from one type to other.  There are two ways to do an update if you want to update the compute.

If all of the computes in your environment are the wrong type for a platform, follow these steps:


1. Disable the entire platform.
2. Commit and deploy.
3. Enable the platform to commit and deploy.

If some computes are deployed by means of a wrong selection or wrong commit, follow these steps:


1. Go to the operation of the instance on the **configure** tab.
2. Click **replace.**
3. Commit and deploy.




## Upgrade Specific OS Packages on a Compute


To update Specific OS packages on a compute:

1. Go to the operation phase of the OS component.
2. Select the instance you want to update with the specific latest OS packages and click **Action**.
    ![Upgrade Specific OS Package Compute](/assets/docs/local/images/upgrade-specific-os-package-on-compute.png)
3. Select upgrade-os-package.
4. Select the package that needs to be upgrade.
5. Select the set size.
6. Start the procedure.
  
    ![Upgrade Specific OS Package Compute New](/assets/docs/local/images/upgrade-specific-os-package-on-compute-new.png)

**This will update the Specified OS packages to the new version available.**

NOTE: All Kernel-related patch updates require a compute reboot. After the packages are installed, do a rolling reboot of computes.

## See Also


* <a href="/user/operation/reboot-computes.html">Reboot Computes</a>
* To query the Kernel pkgs that are installed as part of this activity, use the 
<a href="./grep-or-search-text-in-files-on-computes.html">Grep or Search Text in Files on Computes</a>


## Update OS Packages on a Compute

id: update-os-packages-on-a-compute

To update OS packages on a compute:
 
 
1. Go to the operation phase of the compute component.
2. Select the computes you want to update with latest OS packages and click **Action.**
  
    ![Update OS Package Compute](/assets/docs/local/images/update-os-package-compute.png)
  
3. Select upgrade-os-all.
4. Select the set size.
5. Start the procedure.
  
    ![Update OS Package Compute New](/assets/docs/local/images/update-os-package-compute-new.png)

**This updates the existing OS packages to the new version available and also installs any new packages which are required.**

NOTE: All Kernel-related patch updates require a compute reboot. After the packages are installed, do a rolling reboot of computes.


## Update the Size of a Compute

At this time, you can not update the size (Instance Types) of a compute from one type to other.  There are two ways to do an update if you want to update the compute.

If all of the computes in your environment are the wrong type for a platform, follow these steps:


1. Disable the entire platform.
2. Commit and deploy.
3. Enable the platform to commit and deploy.

If some computes are deployed by means of a wrong selection or wrong commit, follow these steps:


1. Go to the operation of the instance on the **configure** tab.
2. Click **replace.**
3. Commit and deploy.



## ssh a VM
i
1. Go to your design.
2. Modify the component user-app to add to the "Authorized Keys" attribute. 
  
    The value will be the public keys of the users (cat ~/.ssh/id_rsa.pub) who need to have ssh access to your VM. 
  
3. Add one key at a time and click plus sign to add for more users.
4. Save the design changes and commit.
5. Go to Transition.
6. Click **pull the design** in the environment where the VM is.
7. Deploy. (Only the user-app step is executed again.)
8. At a successful deploy, you can log into the VM by doing ssh app@<ip-of-vm>.
  

## SSH to a Compute Node

1. Go to your **Assembly** and select the **Edit the User** component (for example, `user_app`) to add your public keys to the Authorized Keys attribute.
2. If your platform doesn’t have a user component, add one from the component panel on the right side by clicking the **+** next to the user.
3. Get the public key of the user (`cat ~/.ssh/id_rsa.pub`) who needs to have SSH access to your compute (VM).
4. Add one key at a time and click **+** to add more users.
5. Save the design changes and click **Commit.** 
6. Go to **Transition.** 
7. In the environment where the VM is, click **Pull the design.** 
6. Deploy the changes. (Only the user-app step is executed again.)
7. At a successful deploy, you can SSH to the VM by entering:

```
$ ssh <user-name-you-chose>@<ip-of-vm>
```


## Find the hostname of a VM
id: find-hostname-of-vm

The hostname for each VM is dynamically composed in this format:

```
<platform_name>-<cloud_id>-<compute_index>-<compute_id>
```

where:

* **platform_name:** Name of the platform in your design
* **cloud_id:** Internal unique OneOps ciId of the cloud where the VM is deployed
* **compute_index:** Integer index of the compute component in that platform in that cloud
* **compute_id:** Internal unique OneOps ciId of the compute instance

Example:  portal-4349532-1-5107200



## Find the IP Address for a Compute Node

id: find-ip-address-for-compute-node

To find the IP address of a compute node, follow these steps:


1. Click **Operate.**
2. Select the environment.
3. Select the platform.
4. Select the compute component from the list.
5. To find the public IP field of each compute and select its **configuration** tab.

CAUTION: A node's IP Address may change, so you need to make sure that you do not build in reliance on an IP address in your application or operations. Think of an IP Address in OneOps as a PID (a process ID number). Whenever a compute goes through repair or replace activities, the compute may come out with a new IP Address.



##  Fix Unresponsive Compute

id: fix-unresponsive-compute

To fix an unresponsive compute, follow these steps to reboot the compute:


1. Issues a reboot action from the operations of the compute component.
  
    ![Reboot Compute](/assets/docs/local/images/reboot-compute.png)
  
2. If the compute does not respond after the reboot, replace the compute. For instructions on how to replace a compute, go to <a href="#replace-a-bad-vm">Replace a Bad VM</a>.
3. If it is not an option to replace the compute, contact your OneOps administrator for further assistance to bring the node up. 

## Reboot Computes

id: reboot-computes

To reboot computes in OneOps:

1. Go to the operation phase of the compute component.
2. Select the computes you want to reboot and then click **Action**.
  
    ![Reboot Computes](/assets/docs/local/images/reboot-computes.png)
  
3. Select **reboot.**
4. Select the set size.
5. Start the procedure.
6. To do only 50% at a time, select **50** for the step size and deploy.
  
>If 100% is selected, then all of the computes are restarted at the same time.
  
![Reboot Computes New](/assets/docs/local/images/reboot-computes-new.png)




## Replace a Bad VM

Replacing a VM results in the loss of any data available with that VM, for example, log files etc. If you are replacing the VM for a Database or Cache, check with the respective teams before replacing the compute. Additionally, the IP address will change.

Below are the instructions to replace any VM instance when you need to. An example of when you might need to replace a bad VM would be if your team concludes that the failed VM instance cannot be restored for long time or ever. Replacements will generate new IP addresses so any time you do this you need to make sure the Nagios monitoring is adjusted.


1. Make sure that there is no active or pending deployment for the environment.
2. Go to Operations and then to the compute instance that is unhealthy and needs to be replaced. 
3. Select the **configuration** tab and click **Replace.** (Note that this only marks the VM for replacement in OneOps. It does not initiate the actual replacement immediately.)
4. To replace multiple VMs at a time, repeat steps 2 and 3 for any VM you need to replace. Also, you can do step 5 and perform the replacements for some of them before doing others.
  
    **Bulk Replace:** As an alternative to repeating steps 2, 3, and 4, for every instance to be replaced, a multi-select bulk replace operation is available in the component (instance list). Any instance that is already marked for replacement has a purple marker. To do a replace for additional instances, multi-select the instances and then select **replace** from the top-right list menu. The process is exactly the same as selecting individual instances to be replaced. This step only marks/prepares the instances for replacements. The actual replacement is done with the steps below.
  
5. To generate a deployment plan with the replacements steps, go to Operations to the top of the environment summary page and click **Force Deploy.** (Items in the plan have the left green arrow icon in the deployment overlay.)
6. Deploy.

>There is also an “Unreplace” button to unmark the VM should you change your mind before step (6). Once the deployment is kicked off, then it has to be completed.
Obviously the success of the replacement depends on the state of the OpenStack cloud. If there is a bad hypervisor, the Elastic Cloud team needs to ensure that it is disabled so that any new VM replacements do not get allocated to it and fail.



##  Check Status, Repair and Restart a VM

id: check-status-repair-restart-vm

To perform all restarts, starts, stops and repairs in the Operate phase of OneOps, follow these steps:

1.  In the Dashboard in the OneOps organization, select the assembly.
  
    ![Check Status Dashboard](/assets/docs/local/images/check-status-dashboard.png)
  
2. Click Operate. 
  
    ![Check Status Operate](/assets/docs/local/images/check-status-operate.png)  
    The Environments page displays.
  
    ![Check Status Environments](/assets/docs/local/images/check-status-environments.png)  
  
3. Select your environment (usually Prod).
  
    The Environments page defaults to the summary tab.  
    ![Check Status Summary](/assets/docs/local/images/check-status-summary.png)
  
4. Click **graph.**
    
    A graph displays all processes and instances for the selected environment.
    
    >Where the graph displays more components than are easily visible, refer to the component list on the right side of the page.
    
    ![Check Status Graph](/assets/docs/local/images/check-status-graph.png)
    
5. Click the circle icon associated with the compute (VM) you want to restart (start, stop or repair). The Compute Instance page displays your selected instance.
    
    ![Check Status Instance](/assets/docs/local/images/check-status-compute-instance.png)
    
6. Click an action from the Actions panel:
  
  * Status
  * Reboot
  * Upgrade-os-security (Until further notice, NOC analysts will not select this action)
  * Repair
  * Upgrade-os-all (Until further notice, NOC analysts will not select this action)
  
    A confirmation message displays asking you to start your action.
  
    ![Check Status Confirmation](/assets/docs/local/images/check-status-confirmation.png)
  
7. Click **Start Now.**


