# How to use Plaster to generate your code

## Before you begin...

## > Install Plaster
Plaster is completely open source and hosted on the PowerShell Team’s [Github](https://github.com/PowerShell/Plaster). We can grab the most 
recent version from the PowerShell gallery using the below command.

```
Install-Package -Name Plaster -Source PSGallery -Verbose -Force -ForceBootstrap
````

## > Install PowerShell tools for Visual Studio

This is a collection of utilities and project definitions that will simplify
your PowerShell development. Click on the image below to learn more.

<a href="https://poshtools.com"><img src="./media/Poshtools.png" /> </a>

## Getting started...
In our source tree, you will see a plastertemplates folder

<img src="./media/PlasterTemplatesFolder.png" alt="Plaster template folder hiearchy" />

Each folder has a corresponding PlasterManifest.xml and [Folder]Template.ps1 file.

The **[Folder]Template.ps1** file contains the template for the specific functionality that is being created

For each template, there will be additional sections that will need to addressed manually. They are denoted by **# TODO** tags
in the generated code.

Finally, depending upon what destination folder you specify, you may have to manually move the generated file to
its correct location in your source tree.

## Create a project folder
Detailed instruction on how to use Plaster to generate a folder hierarch for your project, can
be found [here](https://github.com/onpremdiag/SharePoint/blob/master/docs/NewProduct.md).

## Create an insight
To create an insight using Plaster, execute the following:

```
Invoke-Plaster 
           -TemplatePath <path to plastertemplates folder>\analyzer 
           -Destination <path to destination folder>
           -ID ([guid]::NewGuid())
           -Name <InsightNameGoesHere>
           -Description "description goes here"
```

This will produce an insight file using the insight template.
````
PS> Invoke-plaster -TemplatePath .\plastertemplates\insight\ -DestinationPath . -ID ([guid]::NewGuid()) -Name RuleDidNotWork -Description "This is for when the rule does not work"
  ____  _           _
 |  _ \| | __ _ ___| |_ ___ _ __
 | |_) | |/ _` / __| __/ _ \ '__|
 |  __/| | (_| \__ \ ||  __/ |
 |_|   |_|\__,_|___/\__\___|_|
                                            v1.1.3
==================================================
Author (Mike McIntyre):
Email (mmcintyr@microsoft.com):
Destination path: C:\Repos\OnPremDiag
   Create IDRuleDidNotWork.ps1
````

This will generate the file, IDRuleDidNotWork.ps1, in the destination folder.
```powershell
################################################################################
# MIT License
#
# Copyright (c) 2019 Microsoft and Contributors
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# Filename: IDRuleDidNotWork.ps1
# Description: This is for when the rule does not work
# Owner: Mike McIntyre <mmcintyr@microsoft.com>
################################################################################
Set-StrictMode -Version Latest

class IDRuleDidNotWork : InsightDefinition
{
    IDRuleDidNotWork()
    {
        $this.Name      = 'IDRuleDidNotWork'

        # TODO - Make sure there is an entry for 'IDRuleDidNotWork' in
        #   InsightActions.en-US.resx
        #   InsightDetections.en-US.resx
        #
        $this.Action    = $global:InsightActions.GetString($this.Name)
        $this.Detection = $global:InsightDetections.GetString($this.Name)

        $this.Id        = [guid]::new('dc7c4630-cba6-4520-adef-8f8a83413905')
        $this.Status    = [OPDStatus]::ERROR
    }

    IDRuleDidNotWork([OPDStatus] $Status)
    {
        $this.Name      = 'IDRuleDidNotWork'

        # TODO - Make sure there is an entry for 'IDRuleDidNotWork' in
        #   InsightActions.en-US.resx
        #   InsightDetections.en-US.resx
        #
        $this.Action    = $global:InsightActions.GetString($this.Name)
        $this.Detection = $global:InsightDetections.GetString($this.Name)

        $this.Id        = [guid]::new('dc7c4630-cba6-4520-adef-8f8a83413905')
        $this.Status    = $Status
    }
}
```

## Create a rule
To create an insight using Plaster, execute the following:
~~~
PS> Invoke-plaster -TemplatePath .\plastertemplates\rule\ -DestinationPath . -ID ([guid]::NewGuid()) -Name MyRule -Description "Checks to see if something happens"
  ____  _           _
 |  _ \| | __ _ ___| |_ ___ _ __
 | |_) | |/ _` / __| __/ _ \ '__|
 |  __/| | (_| \__ \ ||  __/ |
 |_|   |_|\__,_|___/\__\___|_|
                                            v1.1.3
==================================================
Author (Mike McIntyre):
Email (mmcintyr@microsoft.com):
Destination path: C:\Repos\OnPremDiag
   Create RDMyRule.ps1
~~~

This will generate the file, RDMyRule.ps1, in the destination folder.
```powershell
################################################################################
# MIT License
#
# Copyright (c) 2019 Microsoft and Contributors
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# Filename: RDMyRule.ps1
# Description: Checks to see if something happens
# Owner: Mike McIntyre <mmcintyr@microsoft.com>
################################################################################
Set-StrictMode -Version Latest

class RDMyRule : RuleDefinition
{
    RDMyRule([object] $Insight)
    {
        $this.Name        ='RDMyRule'

        # TODO - Make sure there is an entry for 'RDMyRule' in
        # RuleDescriptions.en-US.resx
        $this.Description = $global:RuleDescriptions.GetString($this.Name)

        $this.ExecutionId = [guid]::Empty
        $this.Id          = [guid]::new('b7e7ea84-cc16-4c15-9ca6-ecd5abb45607')
        $this.Success     = $true
        $this.Insight     = $Insight
        $this.EventId     = Get-EventId($this.Name)
    }

    [void] Execute([object] $obj)
    {
        $global:CurrentRule = $this.Id

        # TODO
        # Logic for checking the rule goes here
        #

        # TODO
        # If rule fails, set the following appropriately:
        #   $this.Success = $false
        #
        #   If the insight requires formatting, do so here
        #   $this.Insight.Detection = $this.Insight.Detection -f <parm1> ...
        #   $this.Insight.Action    = $this.Insight.Action -f <parm1> ...
        #

        Write-OPDEventLog -Rule $this
    }
}
```

## Create an analyzer
To create an insight using Plaster, execute the following:

```
PS> Invoke-plaster -TemplatePath .\plastertemplates\analyzer\ -DestinationPath . -ID ([guid]::NewGuid()) -Name MyAnalyzer -Description "Verifies that something is working"
  ____  _           _
 |  _ \| | __ _ ___| |_ ___ _ __
 | |_) | |/ _` / __| __/ _ \ '__|
 |  __/| | (_| \__ \ ||  __/ |
 |_|   |_|\__,_|___/\__\___|_|
                                            v1.1.3
==================================================
Author (Mike McIntyre):
Email (mmcintyr@microsoft.com):
Destination path: C:\Repos\OnPremDiag
   Create ADMyAnalyzer.ps1
```
This will generate the file, ADMyAnalyzer.ps1, in the destination folder.
```powershell
################################################################################
# MIT License
#
# Copyright (c) 2019 Microsoft and Contributors
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# Filename: ADMyAnalyzer.ps1
# Description: Verifies that something is working
# Owner: Mike McIntyre <mmcintyr@microsoft.com>
################################################################################
Set-StrictMode -Version Latest

class ADMyAnalyzer : AnalyzerDefinition
{
    ADMyAnalyzer()
    {
        $this.Name        = 'ADMyAnalyzer'

        # TODO - Make sure there is an entry for 'ADMyAnalyzer' in
        # AnalyzerDescriptions.en-US.resx
        $this.Description = $global:AnalyzerDescriptions.GetString($this.Name)

        $this.Id          = [guid]::new('2727b8f2-e5a1-425a-b9e8-52ffcfac05af')
        $this.Success     = $true
        $this.Executed    = $false
        $this.EventId     = Get-EventId($this.Name)

        # TODO - add the rules that this analyzer will use
        #
        # $this.RuleDefinitions = @([RDRuleDefinition]::new([IDInsightWhenFails]::new()))
        #    or
        # $this.RuleDefinitions = @(
        #   [RDRuleNumber1]::new([IDInsightForRuleNumber1]::new()),
        #   [RDRuleNumber2]::new([IDInsightForRuleNumber2]::new())
        # )
        #
        $this.RuleDefinitions = @()
    }

    [void] Execute([object] $obj)
    {
        $global:CurrentAnalyzer = $this.Id

        foreach($rule in $this.RuleDefinitions)
        {
            $rule.ExecutionId = $this.ExecutionId

            Invoke-Rule -rule $rule -Obj $Obj

            $this.Success = $this.Success -band $rule.Success

            if($false -eq $rule.Success)
            {
                $this.Results += $rule
            }
        }

        Write-OPDEventLog -Analyzer $this

        $this.Executed = $true
    }
}
```
## Create a scenario
To create a scenario using Plaster, execute the following:
```
PS> Invoke-plaster -TemplatePath .\plastertemplates\scenario\ -DestinationPath . -ID ([guid]::NewGuid()) -Name MyScenario -Description "My application is busted"
  ____  _           _
 |  _ \| | __ _ ___| |_ ___ _ __
 | |_) | |/ _` / __| __/ _ \ '__|
 |  __/| | (_| \__ \ ||  __/ |
 |_|   |_|\__,_|___/\__\___|_|
                                            v1.1.3
==================================================
Author (Mike McIntyre):
Email (mmcintyr@microsoft.com):
Destination path: C:\Repos\OnPremDiag
   Create SDMyScenario.ps1
```
This will generate the file, SDMyScenario.ps1, in the destination folder.
```powershell
################################################################################
# MIT License
#
# Copyright (c) 2019 Microsoft and Contributors
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#
# Filename: SDMyScenario.ps1
# Description: My application is busted
# Owner: Mike McIntyre <mmcintyr@microsoft.com>
################################################################################
Set-StrictMode -Version Latest

class SDMyScenario : ScenarioDefinition
{
    SDMyScenario([guid] $ExecutionId)
    {
        $this.Name         = 'SDMyScenario'

        # TODO - Make sure there is an entry for 'SDMyScenario' in
        # ScenarioDescriptions.en-US.resx
        $this.Description  = $global:ScenarioDescriptions.GetString($this.Name)

        $this.$ExecutionId = $ExecutionId
        $this.Id           = [guid]::new('779e99c9-e3f0-4c6a-8afd-5f10022efe94')
        $this.Success      = $true
        $this.EventId      = Get-EventId($this.Name)

        # TODO - add the analyzer(s) that this scenario will use
        #
        # $this.AnalyzerDefinitions = @([ADAnalyzerDefinition]::new())
        #    or
        # $this.AnalyzerDefinitions = @(
        #   [ADNumber1]::new(),
        #   [ADNumber2]::new()
        # )
        #
        $this.AnalyzerDefinitions = @()

        # TODO
        # Optional: A string array of keywords associated with this scenario
        # This will make it easier to search for relevant scenarios
        $this.Keywords = @()

        # TODO - what areas is this scenario applicable to? You will find
        # a list of areas in the config.json file for this product. If the
        # area is not currently defined, add it to the file
        #
        # Make sure there is a corresponding entry in the following:
        #   AreaDescriptions.en-US.resx
        #   AreaTitles.en-US.resx
        #
        # $this.Areas = @($global:AreaTitles.GetString('AreaName'))
        #
        $this.Areas = @()
    }

    [void] Execute()
    {
        $global:CurrentScenario = $this.Id

        # Iterate through each of the analyzers and let them run their rules
        foreach($analyzer in $this.AnalyzerDefinitions)
        {
            $analyzer.ExecutionId = $this.ExecutionId

            Invoke-Analyzer -analyzer $analyzer

            $this.Success = $this.Success -band $analyzer.Success
            if ($false -eq $analyzer.Success)
            {
                $this.Results += $analyzer
            }
        }

        Write-OPDEventLog -Scenario $this
    }
}

```
