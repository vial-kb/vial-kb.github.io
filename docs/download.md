---
layout: page
title: Download
permalink: /download/
nav_order: 5
version: v0.5.2
dl_win_installer: https://github.com/vial-kb/vial-gui/releases/download/v0.5.2/Vial-v0.5.2-setup.exe
dl_win_portable: https://github.com/vial-kb/vial-gui/releases/download/v0.5.2/Vial-v0.5.2-portable.zip
dl_mac: https://github.com/vial-kb/vial-gui/releases/download/v0.5.2/Vial-v0.5.2.dmg
dl_linux: https://github.com/vial-kb/vial-gui/releases/download/v0.5.2/Vial-v0.5.2-x86_64.AppImage
---

# Download Vial

Beta version {{ page.version }}
{: .label .label-yellow .ml-0 }

Currently Vial is in beta. Please report any bugs you encounter to our [issue tracker](https://github.com/vial-kb/vial-gui/issues).

<div id="dl-windows" style="display: none">
<a href="{{ page.dl_win_installer }}" class="btn gettingStarted blue">Windows (installer)</a>
<a href="{{ page.dl_win_portable }}" class="btn gettingStarted">Windows (portable)</a>
<a href="https://github.com/vial-kb/vial-gui" class="btn gettingStarted">Source code</a>
</div>
<div id="dl-mac" style="display: none">
<a href="{{ page.dl_mac }}" class="btn gettingStarted blue">macOS (dmg)</a>
<a href="https://github.com/vial-kb/vial-gui" class="btn gettingStarted">Source code</a>
</div>
<div id="dl-linux" style="display: none">
<a href="{{ page.dl_linux }}" class="btn gettingStarted blue">Linux (AppImage)</a>
<a href="https://github.com/vial-kb/vial-gui" class="btn gettingStarted">Source code</a>
</div>

<script>
function getOperatingSystem() {
  var os = "";
  var ver = window.navigator.appVersion;
  if (ver.indexOf('Win') !== -1) { os = 'windows'; }
  else if (ver.indexOf('Mac') !== -1) { os = 'mac'; }
  else if (ver.indexOf('X11') !== -1 || ver.indexOf('Linux') !== -1) { os = 'linux'; }
  return os;
}

var os = getOperatingSystem();
if (os)
    document.getElementById("dl-" + os).style.display = 'block';
</script>

## Other downloads

- <a href="{{ page.dl_win_installer }}">Windows (installer)</a>
- <a href="{{ page.dl_win_portable }}">Windows (portable)</a>
- <a href="{{ page.dl_mac }}">macOS (dmg)</a>
- <a href="{{ page.dl_linux }}">Linux (AppImage)</a>
- [Source code](https://github.com/vial-kb/vial-gui)
