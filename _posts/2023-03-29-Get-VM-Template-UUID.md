---
published: true
header:
  overlay_image: #/assets/images/rocky-mtns.jpg
  caption: #"[CC License](https://creativecommons.org)"
categories:
        #- Testing
---
# Get VM Template UUID for Use with Terraform
I was creating a terraform file that clones a template.  The VMWare Provider from Terraform requires the UUID of the template.  This info, unfortunately isn't easy to find.  

I settled on using powerCLI.  After logging in it is fairly easy to list the VMs and Templates.
![VMsTemplates](/assets/images/listvm-templates.png)

Using the `get-view` module you can see some of the details of the template.
![GetViewDetail](/assets/images/get-template-get-view.png)

Seeing that there is more nested data in the 'VMware.Vim.VirtualMachineConfigInfo' section I was struggling to figure out how to dig into that data to find if the UUID was even available. 
![GetViewConfig](/assets/images/get-view-getconfig.png)

I normally view pretty much anything older than 5ish years too old to be relevant, but that bit me this time. Surprisingly enough, it was a post in the VMWare communities forums from 2008 that gave what was needed.
https://communities.vmware.com/t5/VMware-PowerCLI-Discussions/How-to-get-the-VM-UUID/td-p/1045158

While this was for the detail from a VM, it works equally as well for a template.

I was able to use this to incrementally dig into the various objects to find the UUID.
![GetConfigDetail](/assets/images/getconfig-detail.png)

If you want the single command that gives the UUID directly:
![GetUUID](/assets/images/getconfig-uuid.png)



<script src="https://utteranc.es/client.js"
        repo="shaunandersonaz/shaunandersonaz.github.io"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script>

