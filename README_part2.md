# Azure Virtual Machine Creation used to host an Active Directory Domain Controller (part 2)


<p>Welcome back to <em>Deploying an Active Directory server using Microsoft Azure Virtual Machines (pt 2)</em>. In part 1 we setup two VMs (Server2019 and Windows10). We won&#8217;t be doing anything with the Windows10 VM but focusing on deploying Active Directory (AD) on Server2019. Let&#8217;s get to it!</p>



<p>From the Azure Dashboard you can see our two VMs under Resources. Click on Server2019:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-42.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4682&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1073,&quot;targetHeight&quot;:1264,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img decoding="async" width="1073" height="1264" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-42.png" alt="" class="wp-image-4682" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-42.png 1073w, https://aaronguild.net/wp-content/uploads/2024/04/image-42-255x300.png 255w, https://aaronguild.net/wp-content/uploads/2024/04/image-42-869x1024.png 869w, https://aaronguild.net/wp-content/uploads/2024/04/image-42-768x905.png 768w" sizes="(max-width: 1073px) 100vw, 1073px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Start Server2019 (<em>refresh screen for status checks. you might get a message across screen stating it&#8217;s not ready, but in the Notifications in top right it states it&#8217;s ready</em>):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-43.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4686&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-43.png" alt="" class="wp-image-4686" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-43.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-43-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-43-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-43-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-43-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Connect to Server2019 via RDP (Connect button &gt; Download RDP file &gt; Open &gt; etc):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-44.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4689&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-44.png" alt="" class="wp-image-4689" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-44.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-44-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-44-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-44-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-44-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>This brings us to the Server Manager &gt; Dashboard:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-45.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4690&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1895,&quot;targetHeight&quot;:984,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1895" height="984" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-45.png" alt="" class="wp-image-4690" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-45.png 1895w, https://aaronguild.net/wp-content/uploads/2024/04/image-45-300x156.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-45-1024x532.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-45-768x399.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-45-1536x798.png 1536w" sizes="(max-width: 1895px) 100vw, 1895px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>In part 1, we&#8217;ve already renamed the Domain Controller from Server2019 to Miami-01. Now we will add some roles and features to this domain controller. In the top right go to Manage &gt; Add Roles and Features:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-46.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4693&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1895,&quot;targetHeight&quot;:984,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1895" height="984" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-46.png" alt="" class="wp-image-4693" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-46.png 1895w, https://aaronguild.net/wp-content/uploads/2024/04/image-46-300x156.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-46-1024x532.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-46-768x399.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-46-1536x798.png 1536w" sizes="(max-width: 1895px) 100vw, 1895px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Hit Next:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-47.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4695&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1085,&quot;targetHeight&quot;:792,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1085" height="792" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-47.png" alt="" class="wp-image-4695" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-47.png 1085w, https://aaronguild.net/wp-content/uploads/2024/04/image-47-300x219.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-47-1024x747.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-47-768x561.png 768w" sizes="(max-width: 1085px) 100vw, 1085px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select <strong>Role-based or feature-based installation &gt; Next</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-49.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4700&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1043,&quot;targetHeight&quot;:783,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1043" height="783" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-49.png" alt="" class="wp-image-4700" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-49.png 1043w, https://aaronguild.net/wp-content/uploads/2024/04/image-49-300x225.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-49-1024x769.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-49-768x577.png 768w" sizes="(max-width: 1043px) 100vw, 1043px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select <strong>Next</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-50.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4702&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1050,&quot;targetHeight&quot;:791,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1050" height="791" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-50.png" alt="" class="wp-image-4702" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-50.png 1050w, https://aaronguild.net/wp-content/uploads/2024/04/image-50-300x226.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-50-1024x771.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-50-768x579.png 768w" sizes="(max-width: 1050px) 100vw, 1050px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select <strong>Active Directory Domain Services</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-51.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4704&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1047,&quot;targetHeight&quot;:796,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1047" height="796" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-51.png" alt="" class="wp-image-4704" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-51.png 1047w, https://aaronguild.net/wp-content/uploads/2024/04/image-51-300x228.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-51-1024x779.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-51-768x584.png 768w" sizes="(max-width: 1047px) 100vw, 1047px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p></p>



<p>When you add the role it will automatically add additional features. Just click <strong>Add Features</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-52.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4705&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1028,&quot;targetHeight&quot;:791,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1028" height="791" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-52.png" alt="" class="wp-image-4705" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-52.png 1028w, https://aaronguild.net/wp-content/uploads/2024/04/image-52-300x231.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-52-1024x788.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-52-768x591.png 768w" sizes="(max-width: 1028px) 100vw, 1028px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Next on Server Roles screen:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-53.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4707&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1049,&quot;targetHeight&quot;:785,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1049" height="785" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-53.png" alt="" class="wp-image-4707" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-53.png 1049w, https://aaronguild.net/wp-content/uploads/2024/04/image-53-300x224.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-53-1024x766.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-53-768x575.png 768w" sizes="(max-width: 1049px) 100vw, 1049px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Next on <strong>Features</strong> tab (notice the <strong>Group Policy Management </strong>feature has been added):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-55.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4710&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1070,&quot;targetHeight&quot;:794,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1070" height="794" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-55.png" alt="" class="wp-image-4710" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-55.png 1070w, https://aaronguild.net/wp-content/uploads/2024/04/image-55-300x223.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-55-1024x760.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-55-768x570.png 768w" sizes="(max-width: 1070px) 100vw, 1070px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Next on the AD DS screen:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-56.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4713&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1060,&quot;targetHeight&quot;:793,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1060" height="793" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-56.png" alt="" class="wp-image-4713" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-56.png 1060w, https://aaronguild.net/wp-content/uploads/2024/04/image-56-300x224.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-56-1024x766.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-56-768x575.png 768w" sizes="(max-width: 1060px) 100vw, 1060px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Install:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-57.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4716&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1029,&quot;targetHeight&quot;:776,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1029" height="776" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-57.png" alt="" class="wp-image-4716" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-57.png 1029w, https://aaronguild.net/wp-content/uploads/2024/04/image-57-300x226.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-57-1024x772.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-57-768x579.png 768w" sizes="(max-width: 1029px) 100vw, 1029px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>The install could take a couple of minutes:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-58.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4718&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:787,&quot;targetHeight&quot;:559,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="787" height="559" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-58.png" alt="" class="wp-image-4718" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-58.png 787w, https://aaronguild.net/wp-content/uploads/2024/04/image-58-300x213.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-58-768x546.png 768w" sizes="(max-width: 787px) 100vw, 787px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>When the installation is complete, click <strong>Promote this server to a domain controller</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-60.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4723&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1272,&quot;targetHeight&quot;:804,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1272" height="804" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-60.png" alt="" class="wp-image-4723" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-60.png 1272w, https://aaronguild.net/wp-content/uploads/2024/04/image-60-300x190.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-60-1024x647.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-60-768x485.png 768w" sizes="(max-width: 1272px) 100vw, 1272px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select <strong>Add a new forest</strong> then give any name for the <strong>Root domain name</strong> (I called it infotechaaron.local). Followed by <strong>Next</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-62.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4726&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:992,&quot;targetHeight&quot;:769,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="992" height="769" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-62.png" alt="" class="wp-image-4726" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-62.png 992w, https://aaronguild.net/wp-content/uploads/2024/04/image-62-300x233.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-62-768x595.png 768w" sizes="(max-width: 992px) 100vw, 992px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Type any password you want for Directory Services Restore Mode (DSRM) and click <strong>Next</strong>:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-63.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4729&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:991,&quot;targetHeight&quot;:707,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="991" height="707" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-63.png" alt="" class="wp-image-4729" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-63.png 991w, https://aaronguild.net/wp-content/uploads/2024/04/image-63-300x214.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-63-768x548.png 768w" sizes="(max-width: 991px) 100vw, 991px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Next on DNS Options:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-64.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4734&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:996,&quot;targetHeight&quot;:768,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="996" height="768" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-64.png" alt="" class="wp-image-4734" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-64.png 996w, https://aaronguild.net/wp-content/uploads/2024/04/image-64-300x231.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-64-768x592.png 768w" sizes="(max-width: 996px) 100vw, 996px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>By default the NetBIOS domain name will autofill. Select Next:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-65.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4735&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:996,&quot;targetHeight&quot;:764,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="996" height="764" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-65.png" alt="" class="wp-image-4735" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-65.png 996w, https://aaronguild.net/wp-content/uploads/2024/04/image-65-300x230.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-65-768x589.png 768w" sizes="(max-width: 996px) 100vw, 996px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Select Next on the Paths screen:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-66.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4737&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:992,&quot;targetHeight&quot;:770,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="992" height="770" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-66.png" alt="" class="wp-image-4737" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-66.png 992w, https://aaronguild.net/wp-content/uploads/2024/04/image-66-300x233.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-66-768x596.png 768w" sizes="(max-width: 992px) 100vw, 992px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>On the Review Options screen you have two options for installing AD. You can continue in the wizard by selecting Next, or you can View Script and run that script in PowerShell. If you choose to run the script in PowerShell:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-67.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4739&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:967,&quot;targetHeight&quot;:689,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="967" height="689" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-67.png" alt="" class="wp-image-4739" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-67.png 967w, https://aaronguild.net/wp-content/uploads/2024/04/image-67-300x214.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-67-768x547.png 768w" sizes="(max-width: 967px) 100vw, 967px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Copy the script:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-68.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4740&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:602,&quot;targetHeight&quot;:661,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="602" height="661" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-68.png" alt="" class="wp-image-4740" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-68.png 602w, https://aaronguild.net/wp-content/uploads/2024/04/image-68-273x300.png 273w" sizes="(max-width: 602px) 100vw, 602px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Open PowerShell under admin mode and paste the script in PowerShell&#8217;s CLI and press enter to install.</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-69.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4742&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1129,&quot;targetHeight&quot;:981,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1129" height="981" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-69.png" alt="" class="wp-image-4742" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-69.png 1129w, https://aaronguild.net/wp-content/uploads/2024/04/image-69-300x261.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-69-1024x890.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-69-768x667.png 768w" sizes="(max-width: 1129px) 100vw, 1129px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-71.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4748&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1276,&quot;targetHeight&quot;:888,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1276" height="888" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-71.png" alt="" class="wp-image-4748" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-71.png 1276w, https://aaronguild.net/wp-content/uploads/2024/04/image-71-300x209.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-71-1024x713.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-71-768x534.png 768w" sizes="(max-width: 1276px) 100vw, 1276px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>It will then sign you out. Go and RDP connect in again after a couple minutes:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-72.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4750&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1913,&quot;targetHeight&quot;:959,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1913" height="959" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-72.png" alt="" class="wp-image-4750" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-72.png 1913w, https://aaronguild.net/wp-content/uploads/2024/04/image-72-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-72-1024x513.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-72-768x385.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-72-1536x770.png 1536w" sizes="(max-width: 1913px) 100vw, 1913px" /><button
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



<p>For some reason when I reconnected to the Server2019, it was spending a lot of time on the &#8220;Group Policy Client&#8221;, so be patient as it sets this up:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="721" height="268" src="https://aaronguild.net/wp-content/uploads/2024/04/image-73.png" alt="" class="wp-image-4751" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-73.png 721w, https://aaronguild.net/wp-content/uploads/2024/04/image-73-300x112.png 300w" sizes="(max-width: 721px) 100vw, 721px" /></figure>



<p>FYI: It took about 5 minutes for me to be able to connect to the VM again. Your patience is required lol.</p>



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Ok, I&#8217;m back into Server2019 and Active Directory has been installed:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-74.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4754&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1865,&quot;targetHeight&quot;:956,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1865" height="956" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-74.png" alt="" class="wp-image-4754" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-74.png 1865w, https://aaronguild.net/wp-content/uploads/2024/04/image-74-300x154.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-74-1024x525.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-74-768x394.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-74-1536x787.png 1536w" sizes="(max-width: 1865px) 100vw, 1865px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now go to: Start &gt; Windows Administrative Tools &gt; Active Directory Administrative Center:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-75.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4758&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:996,&quot;targetHeight&quot;:932,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="996" height="932" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-75.png" alt="" class="wp-image-4758" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-75.png 996w, https://aaronguild.net/wp-content/uploads/2024/04/image-75-300x281.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-75-768x719.png 768w" sizes="(max-width: 996px) 100vw, 996px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>When AD Admin Center opens go to the infotechaaron (local) tab:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-76.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4761&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1421,&quot;targetHeight&quot;:753,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1421" height="753" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-76.png" alt="" class="wp-image-4761" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-76.png 1421w, https://aaronguild.net/wp-content/uploads/2024/04/image-76-300x159.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-76-1024x543.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-76-768x407.png 768w" sizes="(max-width: 1421px) 100vw, 1421px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>From you (local) tab, a best practice is to click on <strong>Enable Recycle Bin </strong>(highlighted in blue on the right). What this does is creates a Recycle Bin which an admin can use if they accidentally delete a user. If that happens, just go into your Recycle Bin and re-enable that user (which will place the deleted user back into the same place it was deleted from. All permissions and groups remain intact).</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-77.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4762&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1423,&quot;targetHeight&quot;:749,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1423" height="749" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-77.png" alt="" class="wp-image-4762" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-77.png 1423w, https://aaronguild.net/wp-content/uploads/2024/04/image-77-300x158.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-77-1024x539.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-77-768x404.png 768w" sizes="(max-width: 1423px) 100vw, 1423px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Click OK:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="403" height="145" src="https://aaronguild.net/wp-content/uploads/2024/04/image-78.png" alt="" class="wp-image-4763" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-78.png 403w, https://aaronguild.net/wp-content/uploads/2024/04/image-78-300x108.png 300w" sizes="(max-width: 403px) 100vw, 403px" /></figure>



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Click OK:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="392" height="189" src="https://aaronguild.net/wp-content/uploads/2024/04/image-79.png" alt="" class="wp-image-4767" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-79.png 392w, https://aaronguild.net/wp-content/uploads/2024/04/image-79-300x145.png 300w" sizes="(max-width: 392px) 100vw, 392px" /></figure>



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Refresh the AD Admin Center a couple of times (when Enable Recycle Bin is greyed out, it&#8217;s enabled):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-80.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4769&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1422,&quot;targetHeight&quot;:711,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1422" height="711" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-80.png" alt="" class="wp-image-4769" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-80.png 1422w, https://aaronguild.net/wp-content/uploads/2024/04/image-80-300x150.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-80-1024x512.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-80-768x384.png 768w" sizes="(max-width: 1422px) 100vw, 1422px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Go to Tools &gt; Active Directory Users and Computers:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-81.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4772&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:1894,&quot;targetHeight&quot;:924,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="1894" height="924" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-81.png" alt="" class="wp-image-4772" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-81.png 1894w, https://aaronguild.net/wp-content/uploads/2024/04/image-81-300x146.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-81-1024x500.png 1024w, https://aaronguild.net/wp-content/uploads/2024/04/image-81-768x375.png 768w, https://aaronguild.net/wp-content/uploads/2024/04/image-81-1536x749.png 1536w" sizes="(max-width: 1894px) 100vw, 1894px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>In Active Directory Users and Computers go to <strong>infotechaaron.local &gt; Users</strong> and notice we have a helpdesk user account already created (there is also several Security Groups that have been created):</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-83.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4777&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:813,&quot;targetHeight&quot;:577,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="813" height="577" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-83.png" alt="" class="wp-image-4777" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-83.png 813w, https://aaronguild.net/wp-content/uploads/2024/04/image-83-300x213.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-83-768x545.png 768w" sizes="(max-width: 813px) 100vw, 813px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Next, open PowerShell again under admin mode and we need to import the active directory module by issuing the following command:</p>



<p><strong>import-module activedirectory</strong></p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-84.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4781&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:850,&quot;targetHeight&quot;:284,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="850" height="284" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-84.png" alt="" class="wp-image-4781" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-84.png 850w, https://aaronguild.net/wp-content/uploads/2024/04/image-84-300x100.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-84-768x257.png 768w" sizes="(max-width: 850px) 100vw, 850px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now issue the <strong>get-command new-aduser -syntax</strong> to see all the commands we can use to manage AD (notice the first one to add a new AD user). I&#8217;ll use that command to create a new AD user named Joe by issuing the <strong>new-aduser Joe </strong>command:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-86.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4785&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:923,&quot;targetHeight&quot;:376,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="923" height="376" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-86.png" alt="" class="wp-image-4785" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-86.png 923w, https://aaronguild.net/wp-content/uploads/2024/04/image-86-300x122.png 300w, https://aaronguild.net/wp-content/uploads/2024/04/image-86-768x313.png 768w" sizes="(max-width: 923px) 100vw, 923px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Then go back into Active Directory Users and Computers &gt; Refresh:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-87.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4788&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:737,&quot;targetHeight&quot;:552,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="737" height="552" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-87.png" alt="" class="wp-image-4788" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-87.png 737w, https://aaronguild.net/wp-content/uploads/2024/04/image-87-300x225.png 300w" sizes="(max-width: 737px) 100vw, 737px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Now we can see the new AD user Joe has been created:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-88.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4789&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:728,&quot;targetHeight&quot;:563,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="728" height="563" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-88.png" alt="" class="wp-image-4789" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-88.png 728w, https://aaronguild.net/wp-content/uploads/2024/04/image-88-300x232.png 300w" sizes="(max-width: 728px) 100vw, 728px" /><button
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



<div style="height:49px" aria-hidden="true" class="wp-block-spacer"></div>



<p>So that was a brief tutorial on creating AD user via PowerShell. You just need to make sure to import the active directory module first.</p>



<p>Other useful PowerShell commands are:</p>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<h4 class="wp-block-heading"><strong>whoami</strong></h4>



<p>PS C:\Users\helpdesk&gt; <strong>whoami</strong><br>infotechaaron\helpdesk</p>



<p><em>whoami tells us that we are logged into the user helpdesk on the infotechaaron domain.</em></p>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<h4 class="wp-block-heading"><strong>whoami /fqdn</strong></h4>



<p>PS C:\Users\helpdesk&gt; <strong>whoami /fqdn</strong><br>CN=helpdesk,CN=Users,DC=infotechaaron,DC=local</p>



<p><em>whoami /fqdn tells us a little more such as the Domain Controller is infotechaaron.local</em></p>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Finally, let&#8217;s enable the new AD user Joe&#8217;s account by right-clicking on his name &gt; Enable Account:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-90.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4799&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:734,&quot;targetHeight&quot;:625,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="734" height="625" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-90.png" alt="" class="wp-image-4799" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-90.png 734w, https://aaronguild.net/wp-content/uploads/2024/04/image-90-300x255.png 300w" sizes="(max-width: 734px) 100vw, 734px" /><button
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



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>You&#8217;ll get this error because we need to give the user Joe a password:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="399" height="167" src="https://aaronguild.net/wp-content/uploads/2024/04/image-91.png" alt="" class="wp-image-4800" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-91.png 399w, https://aaronguild.net/wp-content/uploads/2024/04/image-91-300x126.png 300w" sizes="(max-width: 399px) 100vw, 399px" /></figure>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Right-click on the user and select Reset Password:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-92.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4801&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:736,&quot;targetHeight&quot;:557,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="736" height="557" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-92.png" alt="" class="wp-image-4801" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-92.png 736w, https://aaronguild.net/wp-content/uploads/2024/04/image-92-300x227.png 300w" sizes="(max-width: 736px) 100vw, 736px" /><button
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



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Enter any password and hit Enter:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="376" height="250" src="https://aaronguild.net/wp-content/uploads/2024/04/image-93.png" alt="" class="wp-image-4802" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-93.png 376w, https://aaronguild.net/wp-content/uploads/2024/04/image-93-300x199.png 300w" sizes="(max-width: 376px) 100vw, 376px" /></figure>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>You&#8217;ll see this popup if password is successful (hit OK):</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="300" height="147" src="https://aaronguild.net/wp-content/uploads/2024/04/image-94.png" alt="" class="wp-image-4805"/></figure>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>Right-click on Joe again and then Enable Account:</p>



<figure data-wp-context="{&quot;uploadedSrc&quot;:&quot;https:\/\/aaronguild.net\/wp-content\/uploads\/2024\/04\/image-95.png&quot;,&quot;figureClassNames&quot;:&quot;wp-block-image size-full&quot;,&quot;figureStyles&quot;:null,&quot;imgClassNames&quot;:&quot;wp-image-4807&quot;,&quot;imgStyles&quot;:null,&quot;targetWidth&quot;:726,&quot;targetHeight&quot;:563,&quot;scaleAttr&quot;:false,&quot;ariaLabel&quot;:&quot;Enlarge image&quot;,&quot;alt&quot;:&quot;&quot;}" data-wp-interactive="core/image" class="wp-block-image size-full wp-lightbox-container"><img loading="lazy" decoding="async" width="726" height="563" data-wp-init="callbacks.setButtonStyles" data-wp-on--click="actions.showLightbox" data-wp-on--load="callbacks.setButtonStyles" data-wp-on-window--resize="callbacks.setButtonStyles" src="https://aaronguild.net/wp-content/uploads/2024/04/image-95.png" alt="" class="wp-image-4807" srcset="https://aaronguild.net/wp-content/uploads/2024/04/image-95.png 726w, https://aaronguild.net/wp-content/uploads/2024/04/image-95-300x233.png 300w" sizes="(max-width: 726px) 100vw, 726px" /><button
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



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>You&#8217;ll see this popup if successful:</p>



<figure class="wp-block-image size-full"><img loading="lazy" decoding="async" width="237" height="143" src="https://aaronguild.net/wp-content/uploads/2024/04/image-96.png" alt="" class="wp-image-4809"/></figure>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p>That&#8217;s it for part 2. In this tutorial we covered:</p>



<ul>
<li>Configuring and Installing Active Directory on the Server2019 virtual machine</li>



<li>Active Directory Administrative Center</li>



<li>Adding new AD user using PowerShell</li>
</ul>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>



<p class="has-large-font-size"><strong>MAKE SURE TO STOP YOUR VIRTUAL MACHINE!</strong></p>



<div style="height:36px" aria-hidden="true" class="wp-block-spacer"></div>
