# OpenBox

Switch desktops                        Ctrl-Alt-Arrow, Ctrl-F1, Ctrl-F2
Switch windows directionally           Win-Shift-Arrow

Configuration and Keybindings          ~/.config/openbox/rc.xml
Menu                                   ~/.config/openbox/menu.xml

[openbox-actions]: http://openbox.org/wiki/Help:Actions

## Menu Configuration

```xml
<?xml version="1.0" encoding="UTF-8"?>

<openbox_menu xmlns="http://openbox.org/3.4/menu">

<menu id="apps-menu" label="Applications" execute="openbox-pipemenu" />
<menu id="ob-menu" label="Openbox Preferences">
  <item label="Openbox Configuration Manager">
    <action name="Execute">
      <command>obconf</command>
      <startupnotify><enabled>yes</enabled></startupnotify>
    </action>
  </item>
  <item label="Reconfigure Openbox">
    <action name="Reconfigure" />
  </item>
</menu>

<menu id="root-menu" label="Openbox 3">
  <separator label="Openbox 3" />
  <item label="Terminal">
    <action name="Execute">
      <execute>xterm</execute>
    </action>
  </item>
  <item label="Webbrowser">
    <action name="Execute">
      <execute>firefox</execute>
    </action>
  </item>
  <separator />
  <menu id="apps-menu" />
  <menu id="ob-menu" />
  <separator />
  <item label="Log Out">
    <action name="Exit">
      <prompt>yes</prompt>
    </action>
  </item>
</menu>

</openbox_menu>
```
