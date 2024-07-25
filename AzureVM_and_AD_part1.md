<h1>Azure Virtual Machine Creation used to host an Active Directory Domain Controller (part 1)</h1>

 ### YouTube Demonstration - Coming Soon!

<h2>Description</h2>
In this lab we're going to walk through how to deploy two Microsoft Azure virtual machines in which to create an Active Directory home lab Environmert. Configuring and running this lab will definitely help develop your understanding of how active directory and windows networking works, so I'd highly recommend running through it a couple times and then eventually try to build it on your without using this tutorial.
<br />


<h2>Languages and Programs Used</h2>

- <b>PowerShell</b> 
- <b>Microsoft Azure</b>

<h2>Operating Systems Used </h2>

- <b>Windows Server 2019</b> (Domain Controller for Active Directory)
- <b>Windows 10</b> (A client machine to add to Active Directory)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/UbAkoIp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />






# Azure Virtual Machine Creation used to host an Active Directory Domain Controller (part 1)

<p>First thing we need to do is to take advantage of Microsoft Azure&#8217;s Free Tier services: <a href="https://azure.microsoft.com/en-us/free" target="_blank" rel="noreferrer noopener">https://azure.microsoft.com/en-us/free</a>.</p>



<figure class="wp-block-image size-full"><img decoding="async" width="1812" height="1033" src="https://aaronguild.net/wp-content/uploads/2024/04/image-41.png" alt="" class="wp-image-4647" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-41.png 1812w, https://aaronguild.net/wp-content/uploads/2024/04/image-41-300x171.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-41-1024x584.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-41-768x438.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-41-1536x876.png 1536w" sizes="(max-width: 1812px) 100vw, 1812px" /></figure>



<p>Select the &#8220;Start free&#8221; button to sign up to start using the free cloud services and an additional $200 credit towards the non-free cloud services. For verification you&#8217;ll need to provide a credit card. Microsoft will not charge you during this process.</p>



<p><em>NOTE: Throughout this lab, I will be (and you should too) starting and stopping my VMs constantly to avoid using unnecessary resources that come out of my free tier. When finished with your lab, I recommend STOPPING the virtual machines completely (I&#8217;ll show that later).</em></p>



<p>Alrighty then. After signing up, you will be directed to the Microsoft Azure Dashboard. From here select <strong>Virtual machines</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-4.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4544&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1328,&quot;targetHeight&quot;:925,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img decoding="async" width="1328" height="925" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-4.png" alt="" class="wp-image-4544" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-4.png 1328w, https://aaronguild.net/wp-content/uploads/2024/04/image-4-300x209.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-4-1024x713.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-4-768x535.png 768w" sizes="(max-width: 1328px) 100vw, 1328px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Next in the Virtual machines screen, select <strong>Create &gt; Azure virtual machine</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-5.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4546&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-5.png" alt="" class="wp-image-4546" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-5.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-5-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-5-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-5-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-5-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now you will be prompted to configure the virtual machine:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-7.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4549&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1799,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1073" height="1799" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-7.png" alt="" class="wp-image-4549" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-7.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-7-179x300.png 179w, https://aaronguild.net/wp-content/uploads/2024/04/image-7-611x1024.png 611w, https://aaronguild.net/wp-content/uploads/2024/04/image-7-768x1288.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-7-916x1536.png 916w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<p>You need to create a new Resource group (a collection of resources that share the same lifecycle, permissions and policies). I called it <strong>HomeLab</strong></p>



<p>Give the VM a Virtual machine name: <strong>Server2019</strong></p>



<p>Choose and Image: <strong>Windows Server 2019 Datacenter -x64 Gen2 (free services eligible)</strong></p>



<p>In Size field you can specify the amount of CPUs, memory, etc. Just leave it as the default <strong>(free services eligible)</strong></p>



<p>Create a Username and Password for this VM.</p>



<p>Under Select inbound ports, I&#8217;m using Remote Desktop: <strong>RDP (3389)</strong><br>If you&#8217;re using RDP, make sure you to add your windows username to the allowed list of Remote Desktop Users in Computer Management (<em>type &#8220;Computer Management&#8221; in Windows search bar &gt; System Tools &gt; Local Users and Groups &gt; Remote Desktop Users</em>)</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-6.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4548&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:986,&quot;targetHeight&quot;:708,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="986" height="708" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-6.png" alt="" class="wp-image-4548" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-6.png 986w, https://aaronguild.net/wp-content/uploads/2024/04/image-6-300x215.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-6-768x551.png 768w" sizes="(max-width: 986px) 100vw, 986px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<p>Then select the blue <strong>Review + create</strong> button (<em>you may get an error message stating that you cannot run a VM of this size in the selected zone. If so, just change the value in the Availability Zone field</em>)</p>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-8.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full is-resized&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4551&quot;,&quot;imgStyles&quot;:&quot;width:650px;height:auto&quot;,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1799,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full is-resized wp-lightbox-container"><img loading="lazy" decoding="async" width="1073" height="1799" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-8.png" alt="" class="wp-image-4551" style="width:650px;height:auto" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-8.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-8-179x300.png 179w, https://aaronguild.net/wp-content/uploads/2024/04/image-8-611x1024.png 611w, https://aaronguild.net/wp-content/uploads/2024/04/image-8-768x1288.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-8-916x1536.png 916w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<p>Now we&#8217;re on the Review + Create page (<em>notice it tells you the price per hour to run this VM, as well as the Basics we&#8217;ve just configured</em>). If everything looks good, go ahead and select the blue <strong>Create</strong> button at the bottom.</p>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Azure will run several validation checks and if everything passes, you&#8217;ll see a <strong>Deployment is in progress</strong> message. Shortly after we see a new message, <strong>Your deployment is complete</strong>.</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-9.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4552&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-9.png" alt="" class="wp-image-4552" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-9.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-9-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-9-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-9-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-9-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-10.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4554&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-10.png" alt="" class="wp-image-4554" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-10.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-10-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-10-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-10-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-10-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now let&#8217;s create another VM from the Home screen by clicking <strong>Virtual Machines</strong> again:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-11.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4556&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-11.png" alt="" class="wp-image-4556" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-11.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-11-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-11-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-11-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-11-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>On the Virtual machines screen select <strong>Create</strong> &gt; <strong>Azure virtual machine</strong> (<em>notice the vm we created earlier is displayed here</em>):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-12.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4557&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1908,&quot;targetHeight&quot;:488,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1908" height="488" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-12.png" alt="" class="wp-image-4557" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-12.png 1908w, https://aaronguild.net/wp-content/uploads/2024/04/image-12-300x77.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-12-1024x262.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-12-768x196.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-12-1536x393.png 1536w" sizes="(max-width: 1908px) 100vw, 1908px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now for the second VM, is used the following parameters:</p>



<ul>
<li>Resource group (same): <strong>HomeLab</strong></li>



<li>VM name: <strong>Windows10</strong></li>



<li>Availability zone: <strong>Zones 3</strong></li>



<li>Image: <strong>Windows 10 Pro</strong></li>



<li>Size: (<strong>default</strong>)</li>



<li>Username/PW: <strong>Same as previous</strong></li>



<li>Inbound port: <strong>RDP (3389)</strong></li>



<li>Licensing: <strong>Check the box stating you have a valid license </strong>(<em>I will show you how to get a free 30 day license</em>)</li>
</ul>



<p>Click Review + create blue button:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-13.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4559&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1799,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1073" height="1799" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-13.png" alt="" class="wp-image-4559" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-13.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-13-179x300.png 179w, https://aaronguild.net/wp-content/uploads/2024/04/image-13-611x1024.png 611w, https://aaronguild.net/wp-content/uploads/2024/04/image-13-768x1288.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-13-916x1536.png 916w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>The validation passed message will display on the top of your screen if the configuration has met Azure&#8217;s requirements. Go ahead and create:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-14.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4561&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1799,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1073" height="1799" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-14.png" alt="" class="wp-image-4561" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-14.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-14-179x300.png 179w, https://aaronguild.net/wp-content/uploads/2024/04/image-14-611x1024.png 611w, https://aaronguild.net/wp-content/uploads/2024/04/image-14-768x1288.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-14-916x1536.png 916w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Again, you&#8217;ll see the two deployment status messages (<em>you can select the bell in the top right to view the progress in more detail</em>):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-17.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4565&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:1008,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="1008" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-17.png" alt="" class="wp-image-4565" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-17.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-17-300x158.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-17-1024x540.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-17-768x405.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-17-1536x809.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Depending on your internet speed and the speed of the availability zone at the time, it could take anywhere from 30 seconds to 3 minutes for the VM deployment to complete:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-18.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4567&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-18.png" alt="" class="wp-image-4567" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-18.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-18-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-18-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-18-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-18-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Next, navigate to the <strong>Home </strong>screen and go back into <strong>Virtual machines</strong> again and select the first VM we created (<strong>Server2019</strong>):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-19.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4569&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1909,&quot;targetHeight&quot;:479,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1909" height="479" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-19.png" alt="" class="wp-image-4569" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-19.png 1909w, https://aaronguild.net/wp-content/uploads/2024/04/image-19-300x75.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-19-1024x257.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-19-768x193.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-19-1536x385.png 1536w" sizes="(max-width: 1909px) 100vw, 1909px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>This will bring us to the <strong>Overview</strong> of the <strong>Server2019</strong> vm where you&#8217;ll see all settings (VM name and OS, Public IP address, Size of resources, etc&#8230;) that are configured on this vm:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-21.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4571&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-21.png" alt="" class="wp-image-4571" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-21.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-21-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-21-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-21-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-21-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p><strong>Activity log</strong>: on this tab you can create an Activity Log and filter for different events such as: monitoring what users are doing on the vm, system and health events, and much more:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-22.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4572&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1905,&quot;targetHeight&quot;:657,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1905" height="657" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-22.png" alt="" class="wp-image-4572" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-22.png 1905w, https://aaronguild.net/wp-content/uploads/2024/04/image-22-300x103.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-22-1024x353.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-22-768x265.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-22-1536x530.png 1536w" sizes="(max-width: 1905px) 100vw, 1905px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p><strong>Access control (IAM)</strong>: this tab allows you to grant access and assign roles to users:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-23.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4573&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1891,&quot;targetHeight&quot;:715,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1891" height="715" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-23.png" alt="" class="wp-image-4573" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-23.png 1891w, https://aaronguild.net/wp-content/uploads/2024/04/image-23-300x113.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-23-1024x387.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-23-768x290.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-23-1536x581.png 1536w" sizes="(max-width: 1891px) 100vw, 1891px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-24.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4575&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1895,&quot;targetHeight&quot;:601,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1895" height="601" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-24.png" alt="" class="wp-image-4575" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-24.png 1895w, https://aaronguild.net/wp-content/uploads/2024/04/image-24-300x95.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-24-1024x325.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-24-768x244.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-24-1536x487.png 1536w" sizes="(max-width: 1895px) 100vw, 1895px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>I&#8217;m not going to go over all of the tabs but some notable tabs are:</p>



<p><strong>Diagnose and solve problems</strong>: if you have some weird issues going on in your VM you can resolve them here.</p>



<p><strong>Networking Settings</strong>: you could create an inbound outbound rule.</p>



<p><strong>Connect</strong>: used to remote into this machine which we&#8217;re going to do shortly.</p>



<p><strong>Disk</strong>: you could increase the disk size as needed if you need to.</p>



<p><strong>Size</strong>: you could update the memory of the RAM on this if you need to.</p>



<p><strong>Microsoft Defender for Cloud</strong>: used for discovering threats and removing malicious software and viruses.</p>



<p><strong>Backup</strong>: used for backing up the vm.</p>



<p><strong>Reset password</strong>: a common use here is if you&#8217;ve forgotten your password or locked out of your account.</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-25.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4577&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1801,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1073" height="1801" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-25.png" alt="" class="wp-image-4577" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-25.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-25-179x300.png 179w, https://aaronguild.net/wp-content/uploads/2024/04/image-25-610x1024.png 610w, https://aaronguild.net/wp-content/uploads/2024/04/image-25-768x1289.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-25-915x1536.png 915w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p><strong>Server2019 VM:</strong></p>



<p>Now let&#8217;s actually connect to our Server2019 VM by going to Connect, Download RDP file and Open:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-27.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4582&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1907,&quot;targetHeight&quot;:936,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1907" height="936" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-27.png" alt="" class="wp-image-4582" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-27.png 1907w, https://aaronguild.net/wp-content/uploads/2024/04/image-27-300x147.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-27-1024x503.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-27-768x377.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-27-1536x754.png 1536w" sizes="(max-width: 1907px) 100vw, 1907px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Then Connect:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-28.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4583&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:542,&quot;targetHeight&quot;:287,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="542" height="287" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-28.png" alt="" class="wp-image-4583" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-28.png 542w, https://aaronguild.net/wp-content/uploads/2024/04/image-28-300x159.png 300w" sizes="(max-width: 542px) 100vw, 542px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>It will prompt you for your password then hit OK:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-29.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4584&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:456,&quot;targetHeight&quot;:347,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="456" height="347" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-29.png" alt="" class="wp-image-4584" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-29.png 456w, https://aaronguild.net/wp-content/uploads/2024/04/image-29-300x228.png 300w" sizes="(max-width: 456px) 100vw, 456px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Hit Yes when it says identity cannot be verified:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-30.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4585&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:392,&quot;targetHeight&quot;:401,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="392" height="401" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-30.png" alt="" class="wp-image-4585" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-30.png 392w, https://aaronguild.net/wp-content/uploads/2024/04/image-30-293x300.png 293w" sizes="(max-width: 392px) 100vw, 392px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>It will then start loading the VM and go through the basic setup configurations.</p>



<p>Now you should see the Server Manager Dashboard:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-31.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4587&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1917,&quot;targetHeight&quot;:1080,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1917" height="1080" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-31.png" alt="" class="wp-image-4587" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-31.png 1917w, https://aaronguild.net/wp-content/uploads/2024/04/image-31-300x169.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-31-1024x577.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-31-768x433.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-31-1536x865.png 1536w" sizes="(max-width: 1917px) 100vw, 1917px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>First thing I&#8217;ll do is change the date/time to my local time so there&#8217;s no confussion down the line (right click on the date/time at bottom-right of VM screen and select Adjust date/time:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-32.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4590&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1867,&quot;targetHeight&quot;:1047,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1867" height="1047" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-32.png" alt="" class="wp-image-4590" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-32.png 1867w, https://aaronguild.net/wp-content/uploads/2024/04/image-32-300x168.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-32-1024x574.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-32-768x431.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-32-1536x861.png 1536w" sizes="(max-width: 1867px) 100vw, 1867px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Then select your local timezone:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-33.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4592&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1194,&quot;targetHeight&quot;:690,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1194" height="690" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-33.png" alt="" class="wp-image-4592" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-33.png 1194w, https://aaronguild.net/wp-content/uploads/2024/04/image-33-300x173.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-33-1024x592.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-33-768x444.png 768w" sizes="(max-width: 1194px) 100vw, 1194px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Next I&#8217;ll rename this server from <strong>Server2019</strong> to <strong>Miami-01</strong> (File Manager &gt; right-click on This PC &gt; Properties &gt; Change settings &gt; Change &gt; enter new Computer name &gt; OK):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-35.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4594&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1440,&quot;targetHeight&quot;:978,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1440" height="978" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-35.png" alt="" class="wp-image-4594" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-35.png 1440w, https://aaronguild.net/wp-content/uploads/2024/04/image-35-300x204.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-35-1024x695.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-35-768x522.png 768w" sizes="(max-width: 1440px) 100vw, 1440px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Then click OK &gt; Restart Now (VM will disconnect and you&#8217;ll need to RDP back in):</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="348" height="176" src="https://aaronguild.net/wp-content/uploads/2024/04/image-36.png" alt="" class="wp-image-4596" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-36.png 348w, https://aaronguild.net/wp-content/uploads/2024/04/image-36-300x152.png 300w" sizes="(max-width: 348px) 100vw, 348px" /></figure>



<p><em>Note: I could&#8217;ve changed the name of this PC (Server2019) in the initial Azure VM configuration, but knowing how to rename a PC is a basic skill everyone in IT should know how to do.</em> </p>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p><br><strong>Windows10 VM</strong></p>



<p>While that&#8217;s restarting, I&#8217;ll go ahead and connect to the Windows10 VM for the first time by following the exact same process as connecting to the Server2019 VM (download the RDP file &gt; open &gt; enter credentials). Hit &#8220;Accept&#8221; for Privacy Settings on the Windows10 VM:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="1076" height="786" src="https://aaronguild.net/wp-content/uploads/2024/04/image-37.png" alt="" class="wp-image-4619" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-37.png 1076w, https://aaronguild.net/wp-content/uploads/2024/04/image-37-300x219.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-37-1024x748.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-37-768x561.png 768w" sizes="(max-width: 1076px) 100vw, 1076px" /></figure>



<p>Repeat the updating the correct <strong>date/time</strong> process as well as renaming this VM from Windows10 to <strong>Desktop-01</strong>. Restart the VM to apply.</p>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p><strong>Miami-01</strong>:</p>



<p>Reconnect to Miami-01 via rdp.</p>



<p>Once connected, let&#8217;s verify the name change by opening the command prompt and issuing the command: whoami /user</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-38.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4626&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1235,&quot;targetHeight&quot;:1028,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1235" height="1028" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-38.png" alt="" class="wp-image-4626" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-38.png 1235w, https://aaronguild.net/wp-content/uploads/2024/04/image-38-300x250.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-38-1024x852.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-38-768x639.png 768w" sizes="(max-width: 1235px) 100vw, 1235px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Notice the green arrow pointing to the new pc name of <strong>miami-01</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-39.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4628&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:557,&quot;targetHeight&quot;:287,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="557" height="287" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-39.png" alt="" class="wp-image-4628" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-39.png 557w, https://aaronguild.net/wp-content/uploads/2024/04/image-39-300x155.png 300w" sizes="(max-width: 557px) 100vw, 557px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<div style="height:40px" aria-hidden="true" class="wp-block-spacer"></div>



<p>So we are good to go with this VM and go ahead and sign out. This will bring you back to the Azure dashboard.</p>



<p>Select Virtual machines &gt; check the box to the left of Name to select all &gt; Stop both VMs:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-40.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4632&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1906,&quot;targetHeight&quot;:412,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1906" height="412" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-40.png" alt="" class="wp-image-4632" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-40.png 1906w, https://aaronguild.net/wp-content/uploads/2024/04/image-40-300x65.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-40-1024x221.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-40-768x166.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-40-1536x332.png 1536w" sizes="(max-width: 1906px) 100vw, 1906px" /><button
			class="lightbox-trigger"
			type="button"
			aria-haspopup="dialog"
			aria-label="Enlarge image"
			data-wp-init="callbacks.initTriggerButton"
			data-wp-on--click="actions.showLightbox"
			data-wp-style--right="context.imageButtonRight"
			data-wp-style--top="context.imageButtonTop"
		>
			<svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" fill="none" viewBox="0 0 12 12">
				<path fill="#fff" d="M2 0a2 2 0 0 0-2 2v2h1.5V2a.5.5 0 0 1 .5-.5h2V0H2Zm2 10.5H2a.5.5 0 0 1-.5-.5V8H0v2a2 2 0 0 0 2 2h2v-1.5ZM8 12v-1.5h2a.5.5 0 0 0 .5-.5V8H12v2a2 2 0 0 1-2 2H8Zm2-12a2 2 0 0 1 2 2v2h-1.5V2a.5.5 0 0 0-.5-.5H8V0h2Z" />
			</svg>
		</button></figure>



<p><em>Note: I&#8217;m starting and stopping these VMs a lot because we don&#8217;t want to be charged for a VM running while we are not using it. </em></p>
