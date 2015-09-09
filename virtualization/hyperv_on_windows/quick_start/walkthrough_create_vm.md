***PLOC***ms.ContentId: 3C63F9A8-30E4-40F4-BC7B-A001C1E90779
title: Step 4: Create a Windows virtual machine from an .iso file***PLOC***

#***PLOC***Step 4: Create a Windows virtual machine from an .iso file***PLOC***

***PLOC***For this step, if you already have a .iso file for a supported 64-bit operating system, you can use that.***PLOC***
***PLOC***If not, you can download the .iso for ***PLOC***[***PLOC***Windows 8.1 Enterprise***PLOC***](http://www.microsoft.com/en-us/evalcenter/evaluate-windows-8-1-enterprise)***PLOC*** and choose the 64-bit edition.***PLOC***

1.  ***PLOC***In Hyper-V Manager, click on the ***PLOC********PLOC***Action***PLOC********PLOC*** menu > ***PLOC********PLOC***New***PLOC********PLOC*** > ***PLOC********PLOC***Virtual machine***PLOC********PLOC***.***PLOC***
2.  ***PLOC***In the virtual machine wizard, make the following choices:***PLOC***
    
    <table>
      <tr>
        <th caps_internal_Id="27c301c2-6526-4d4c-88d8-cf6706fbc8f7">Page</th>
        <th caps_internal_Id="c357dade-34ea-48fc-9293-6b442ee628ef">Entry</th>
      </tr>
      <tr>
        <td caps_internal_Id="8e72a245-9def-4935-a4a1-1a6bb8a1573d">Name:</td>
        <td>Type in <b caps_internal_Id="3ff6aba5-b97d-4702-b21e-4ba465d46b45">Windows Walkthrough VM</b></td>
      </tr>
      <tr>
        <td caps_internal_Id="72bb8115-d4ac-41aa-998c-d470a79d942f">Generation:</td>
        <td>
          <b caps_internal_Id="48c5265e-e19b-4429-a82c-71e4e878fbcb">Generation 2</b>
        </td>
      </tr>
      <tr>
        <td caps_internal_Id="04d687e7-ead2-4a8f-8ce4-25c9c211b7de">Startup Memory:</td>
        <td>
          <b caps_internal_Id="befdfec4-653a-4d52-9db4-9ba6d77f8517">1024</b> and leave dynamic memory selected</td>
      </tr>
      <tr>
        <td caps_internal_Id="0fa6c0be-26fe-4465-bd0e-f484102efdef">Configure Networking:</td>
        <td>
          <b caps_internal_Id="7b8da996-e11b-4ea6-8484-5d232270173c">External</b> (this is the virtual switch you created in Step 3)</td>
      </tr>
      <tr>
        <td caps_internal_Id="746ec0b1-7ce2-4a35-b5ca-cc45502b5127">Connect virtual hard disk:</td>
        <td>
          <b caps_internal_Id="6b4a45ed-ab3a-4c1d-b8cb-0ab6f682df45">Create a virtual hard disk</b> (keep the other default values) </td>
      </tr>
      <tr>
        <td caps_internal_Id="2be6c599-47c1-4b32-8937-ff119e09dc78">Installation Options:</td>
        <td>
          <b caps_internal_Id="03efb478-5cd7-4b17-a634-e9c79a13fcff">Install an operating system from a bootable CD/DVD-ROM</b>. Under <b caps_internal_Id="f2ad266a-beb4-4602-99e3-3573454a745a">Media</b>, select <b caps_internal_Id="c6cf714e-223d-439d-8e14-523b1a2f990b">Image file (iso)</b> and then click <b caps_internal_Id="2e017058-ebb8-450c-bf7f-03c81df2a0ae">Browse</b> to point to the .iso file.</td>
      </tr>
    </table>
3.  ***PLOC***When everything looks right, click ***PLOC********PLOC***Finish***PLOC********PLOC***.***PLOC***

> *****PLOC***Note:***PLOC********PLOC*** If you only have 32-bit version of Windows, you need to choose Generation 1 in the ***PLOC********PLOC***Generation***PLOC********PLOC*** section of the wizard.***PLOC***
> ***PLOC***Generation 2 VMs only support 64-bit operating systems.***PLOC***
> 

##***PLOC***Next Step:***PLOC***

[***PLOC***Step 5: Connect to the virtual machine and finish the installation***PLOC***](walkthrough_vmconnect.md)


