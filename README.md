ALKS - System architecture with SysML
=============================

The "ALKS Regulation UN R157" ECE/TRANS/WP.29/2020/81 <sup>[[1]](https://undocs.org/ECE/TRANS/WP.29/2020/81)</sup>  is necessary for the approval of an "Automated Lane Keeping System" on motorways presented in the [UNECE Press Release](https://www.unece.org/info/media/presscurrent-press-h/transport/2020/un-regulation-on-automated-lane-keeping-systems-is-milestone-for-safe-introduction-of-automated-vehicles-in-traffic/doc.html).
The Systems Modeling Language (SysML) is a general-purpose modeling language for systems engineering applications. It supports the specification, analysis, design, verification and validation of a broad range of systems and systems-of-systems.<sup>[[2]](https://en.wikipedia.org/wiki/Systems_Modeling_Language)</sup>

# Goal
This project intends to formally describe the system architecture of the Automated Lane Keeping Assistant as defined in UN R157 with the intention to map the necessary tests needed to comply with international regulation and certification of the function to different test instances (e.g. HIL, MIL, SIL). Eventually the tests for software in the loop (SIL) should be executed.

# Requirements and Setup
Clone the repository to your local machine.

Minimum requirements:
- OpenJDK > 15.0.2 [download](https://download.java.net/java/GA/jdk15.0.2/0d1cfde4252546c6931946de8db48ee2/7/GPL/openjdk-15.0.2_windows-x64_bin.zip)
- Eclipse IDE 2020-12 [download](https://www.eclipse.org/downloads/download.php?file=/oomph/epp/2020-12/R/eclipse-inst-jre-win64.exe)
- Papyrus < 5.0.0 (Workbench installation) [download](https://download.eclipse.org/modeling/mdt/papyrus/updates/releases/2020-12/5.0.0/)

## Windows

### OpenJDK
1. Extract the zip file into a folder, e.g. C:\Program Files\Java\ and it will create a jdk-15 folder (where the bin folder is a direct sub-folder). You may need Administrator privileges to extract the zip file to this location.
2. Set JAVA_HOME:
    - Under System Variables, click New.
    - Enter the variable name as JAVA_HOME.
    - Enter the variable value as the installation path of the JDK (without the bin sub-folder).
3. Configure PATH:
    - Select PATH under System Variables.
    - Add the location of the bin folder of the JDK installation to the PATH variable in System Variables.
    - The following is a typical value for the PATH variable: C:\WINDOWS\system32;C:\WINDOWS;"%JAVA_HOME%\bin"
    - Click OK.
    - Click Apply Changes.
4. Add other useful variables as [described here](https://stackoverflow.com/a/26640589/2883130) and look at the optional instructions.

To see if it worked, open up the Command Prompt:
~~~
C:\>java --version
openjdk 15.0.2 2021-01-19
OpenJDK Runtime Environment (build 15.0.2+7-27)
OpenJDK 64-Bit Server VM (build 15.0.2+7-27, mixed mode, sharing)
~~~

If you want to uninstall - just undo the above steps.

### Eclipse

1. Download the Eclipse Installation Package.
2. Run the installation by clicking on the downloaded installation package (usually in the windows-download folder) Note, that administration rights are necessarry.
3. Select Eclipse Modeling Tools, make sure the proxy settings are correct to allow the download of the application components.
4. Launch the application and check, if its running.
5. Select a workspace (you can use the default folder or can browse and create a new one, e.g eclipseworkspace202012, especially if there are older installations of eclipss choose a new one).

### Papyrus

Installation of papyrus and plugins are done in the eclipse tool. If eclipse is not running start it at first.

For installing Papyrus do the following steps:

1. Help -> Install new software -> The install-window opens.
2. Under "work with" fill in the source of the papyrus package: `https://download.eclipse.org/modeling/mdt/papyrus/updates/releases/2020-12/5.0.0/`.
3. Click on the Add... Button.
4. Under "Add Repository" fill in a name (e.g Papyrus 5.0) and click on "Add".
5. The Install window is shown again with the possible plugins for the installation package select there: Papyrus, Papyrus Releng Tools, Papyrus Toolsmith and optionally Papyrus User Examples.
6. Click on "Next" -> Accept the terms of service.
If there are other installations of papyrus it is possible, that the installation run can not be completed, thus try the following
7. If the install window shows "Install Remeditation Page - The install cannot be completed" select the following solution: Keep my installation the same and modify the items being installed to be compatible.
8. A security warning appears: "Warning : Installing unsigned software for witch the authenicity or.....Continue with the installation? Select "Install anyway".
9. A Window appears "Software Updates - Restart Eclipse IDE to apply the software update? Select "Restart now".

### Papyrus-Plugins

For sysml-modelling there are different plugins necessarry to be installed in the follwoing order:
- GMF plugin
- SYSML 1.4 plugin
- EMF compare
- Papyrus compare

Installing the GMF plugin:

1. Choose Help - Install new software.
2. Add the plugin by clicking on Add.. .
3. Fill in the download adress `http://download.eclipse.org/modeling/gmp/gmf-tooling/updates/releases-3.3.1a` and give a name (e.g. GMF).
4. Select the shown plugin and click "Next".
5. A security warning appears: "Warning : Installing unsigned software for witch the authenicity or.....Continue with the installation? Select "Install anyway".
6. A Window appears "Software Updates - Restart Eclipse IDE to apply the software update? Select "Restart now".

Installing the syml 1.4 profile:

1. Choose Help - Eclipse Marketplace.
2. Type in the Search tab, "Find" field: `sysml`.
3. All available plugins for sysml are shown. 
4. Choose SYSML 1.4 by cklicking on the "install" button.
5. If a security warning appears: "Warning : Installing unsigned software for witch the authenicity or.....Continue with the installation? Select "Install anyway".
6. A Window appears "Software Updates - Restart Eclipse IDE to apply the software update? Select "Restart now".

Note: If an error occurs install the proposed packages.

Installing EMF Compare:

1. Choose Help - Eclipse Marketplace.
2. Type in the Search tab, "Find" field: `EMF compare`.
3. All available plugins for comparison are shown Choose "EMF Compare" by clicking the "install" button.
4. Next window shows "Confirm selected Features".
   - Model comparison (required) --> this is already selected.
   - Select "Model comparison - EGit Support".
   - Note: Don't select the "Model comparison - Papyrus Support" --> this plugin must be installed afterwards.
   - Press "Confirm".
5. Press "Finish" and "restart".

Installing Papyrus Compare:

1. Choose Help - Install new software
2. Add the plugin by clicking on Add.. 
3. Fill in the download adress: `https://download.eclipse.org/modeling/mdt/papyrus/components/compare/updates/integration` and give a name (e.g. Papyrus Compare).
4. Select in the main window Papyrus Compare, then press "Next".
5. A window appears with installation details, press "Next".
6. A window "Review Licenses" appears, select "I accept the terms of the license agreements" and press "Finish".
7. A security warning window appears with a warning, press "Install anyway".
8. Window "Software Updates" asks "Restart Eclips IDE to apply the software update?", press "Restart Now".

## Linux
TBD

```bash
sudo apt-get update
sudo apt-get install openjdk-15-jdk
export JAVA_HOME=/usr/lib/jvm/openjdk-15-jdk
export PATH=$PATH:$JAVA_HOME/bin
```

## Show the model

- Open Eclipse
- Window -> Perspective -> Open Perspective -> Other: Select Papyrus
- Open project
