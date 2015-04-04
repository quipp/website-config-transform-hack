<p>
  In Visual Studio, Web Sites don’t support web.config transformation files (i.e. Web.UAT.config) as well as Projects.
</p>
<p>
It turns out Web Sites do support a single web config transformation file (Web.Debug.config).  Works the same as in Web Applications.  However, if you want more than one transformation files for different deployments, you have to use a hack.</p>
<p>
  The sample solution code includes two different publish profiles.  WebDeployTest works (make sure to setup the website with same port on localhost) - uses Web Deploy.  LocalTest deliberatly does not work to demonstrate that deploying to file system will not work.
</p>
<ul>
  <li>Works Visual Studio 2012 or later. (possible VS 2010, but not tested)</li>
  <li>Create new web config transformation file (i.e. Web.Staging.config).</li>
  <li>Create publish profile by going through Publish process for the web site.  This sets of the necessary files (i.e. website.publishproj)<br />
    <ul>
      <li>Must use Web Deploy (to a web site in IIS – can be local).  Does not work if publish to File System.</li>
      <li>Must have a working site in IIS available to use.</li>
    </ul>
  </li>
  <li>To change which web config transformation file is used, change the following in website.publishproj</li>
</ul>
From<br />
`<Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>`
<br />To<br />
`<Configuration Condition=" '$(Configuration)' == '' ">WHATEVER</Configuration>`
<br />Example for Web.Staging.config<br />
`<Configuration Condition=" '$(Configuration)' == '' ">Staging</Configuration>`


    
