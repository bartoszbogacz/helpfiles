# Vnc

Install `Xvnc`

  ssh -L 5901:localhost:5901 dev
  sudo zypper install xorg-x11-Xvnc dbus-1-x11 openbox xterm gvim
  echo "openbox-session" > ~/.xinitrc
  vncserver -fg

Alternatively

  vncserver -autokill

Get TigerVNC [tigervnc]. Connect to VNC server: `localhost:5901`

  xrdb -merge .Xresources
