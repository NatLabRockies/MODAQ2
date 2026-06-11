# Q&A ![MODAQ M2 Q&A](img/m2_icon.png#right)

## How does MODAQ differ from pre-built commercial options?
This is a good question and important to understand where MODAQ fits in with commercial alternatives. Due to a variety of factors, the answer is not that simple. One needs to consider budget, performance expectations, system flexibility, functional requirements, and the technical aptitude of the end user. 

Here's some things to consider:

1. Data acquisition systems can be found ranging from a few hundred dollars to well over $100,000 in cost. The price point is often a clue as to how performant and capable (and complex) the system will likely be.  
2. While some commercial products provide user software to configure, manage, and operate the system, anything beyond the basics will require programming. 
3. If the measurements are important, for instance being used for model validation, design basis, safety, or for financial/production purposes, the quality and integrity of those measurements must be able to withstand scrutiny. 

Data acquisition is an engineering discipline with numerous sub-specialties that can take years and lots of study to become competent. By offering MODAQ publicly, users can leverage the efforts of the national lab 

## Why not just use generic DAQ controllers?
There are a lot of options out there, but it does not take long to realize that:

1. You're just trading one ecosystem for another.
2. Specification to price ratio might be (much) worse.
3. Documentation and libraries may be lacking.
4. Device compatibility may become a bit of an issue.
5. Your preferred programming language or operating system might not be supported.
6. Software still needs to be developed (or in some cases configured) to achieve expected results.
7. It could end up being a lot of work!

Of course it depends on individual needs and expectations, but whether going with MODAQ or an alternative, there's no getting away from the tasks of programming the system and assuring it will perform to expectations and deliver quality results.

Some vendors sell controllers and I/O modules and offer software packages that require some configuration to achieve basic and limited data acquisition that can be considered on the easy end of the spectrum. However, doing anything beyond simple acquisitions often requires accessing a vendor supplied API and writing code in a traditional language like C/C++ or python - or worse - writing code in a vendor developed scripting language.

There's a class of controllers that include an array of built-in I/O that are nice, well thought out, easy to configure, and performant, however under closer inspection, they lack some key features that make them unsuitable in an embedded application deployed in the field. For example, these options generally have limited data logging capability, supporting only small (usually 64 GB or less) and slow microSD cards. There's also limitations when it comes to more technical matters, such as sampling speed, multiplexing (or scanning) vs simultaneous sampling, data synchronization, bit depth, multitasking, determinism, and noise. They also lack flexibility of local filtering or signal processing of data, local QC, and communications/remote supervision. Of course, use case and measurement objectives matter, so these can be perfectly fine for some applications.

## Is MODAQ plug-n-play? 
Generally, no. Each user will have their own unique set of measurement objectives and requirements which cannot realistically be fulfilled by a general MODAQ design. The one exception is the Reference Design presented in the previous sections of this documentation. If the user selects the exact hardware presented in the [Hardware Reference Design section](hardware.md/#hardware-reference-design) and follows the instructions in the [Software section](software.md), the system should function. NLR has a limited number of fully built and configured MODAQ2 Reference Design systems that can be loaned out under the M2GO program. 

## What is M2GO?
M2GO is a fully built, configured, functional, and tested manifestation of the M2 reference design presented in this web document that is available for loan from NLR to qualified 3rd party end users. This is first come, first served and availability is limited. To learn more, contact us <a href="https://www.nlr.gov/water/modaq" target= "_blank">here</a>

## Do I need to know programming to use MODAQ?

## Which sensors or instruments should I use? 
If you have to ask...

## Can NLR help configure or customize MODAQ?

<a href="https://www.nlr.gov/news/video/discovering-the-ocean-through-data-modaq-text.html" target = "_blank">MODAQ</a> is funded by the Department of Energy's <a href="https://www.energy.gov/cmei/water/hydropower-and-hydrokinetic-office" target="_blank">Hydropower and Hydrokinetic Office (H2O)</a> for the purpose of advancing the development and testing of Marine Energy devices.  There are <a href="https://www.nlr.gov/water/work-with-us.html" target="_blank">mechanisms in place</a> for large and small organizations to engage NLR.  