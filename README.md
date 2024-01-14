<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Thanks again! Now go create something AMAZING! :D
***
***
***
*** To avoid retyping too much info. Do a search and replace for the following:
*** github_username, repo_name, twitter_handle, email, project_title, project_description
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#troubleshooting">Troubleshooting</a>
      <ul>
        <li><a href="#pi-camera-and-mainsail-os">Pi Camera and Mainsail OS</a></li>
      </ul>
    </li>
    <li><a href="#odds-and-ends">Odds and Ends</a>
      <ul>
        <li><a href="#using-btt-pi">Using BTT Pi</a></li>
        <li><a href="#bed-leveling">Bed Leveling</a>
          <ul>
            <li><a href="#no-abl">No ABL</a></li>
            <li><a href="#abl">ABL</a></li>
          </ul>
        </li>
      </ul>
    </li>    
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

I recently received an SKR Mini e3 V3.0 from a friend, and decided to upgrade my Ender 3 v1. I replaced the original Creality v4.2.7 board with the SKR and then installed Klipper onto it.

I wanted to pull together a quick tutorial on how I did this, so that it may help someone else in the future.

This is mainly a collection of links and resources, rather than me re=inventing the wheel. I will do my very best to give credit where I can.

Also, I doubt this needs to be said, but I am NOT responsible for any damage that may occur to your hardware or property if you choose to follow this tutorial. Always make sure to research stuff out before slapping down code or upgrades onto your hardware.


### Built With

* [Klipper](https://www.klipper3d.org/)
* [Mainsail OS](https://docs-os.mainsail.xyz/)

<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

* Ender 3
* SKR Mini e3 V3.0
* Raspberry Pi*

*For the sake of this tutorial, I am using an RPi 3+ that I was already using for Octoprint. I was also gifted a BigTreeTech Pi v1.2. However, I chose to stick with the Pi for the time being, since I already have a Pi Camera v2 and a mount for it. I am going to still include references for using the BTT with Klipper on this tutorial.

### Installation

The process I followed was:

1. Install the SKR into the Ender 3.
2. Install Mainsail OS onto the Pi.
3. Flash Klipper on to the SKR.
4. Create printer.cfg within Mainsail.

I followed [YouMakeTech's](https://www.youmaketech.com/how-to-install-klipper-on-the-skr-mini-e3-v3/) tutorial for all of these steps. He does a great job of providing wiring diagrams and instructions.
I also found [MakeNPrint's](https://www.makenprint.uk/3d-printing/3d-printing-guides/3d-printer-mainboard-installation-guides/btt-skr-mini-e3-v3-guides/btt-skr-mini-e3-v3-setup-guide/) SKR guide to be extremely helpful. It goes in-depth on the components of the SKR board.

A few notes:

1. The hotend heat sink fan will have to have a JST 2-pin connector soldered or crimped onto the leads. With the Creality board, this fan connects directly into a wire terminal, rather than a board connector. However, a JST 2-pin connector is needed to connect it to the SKR board.
2. The fan connections listed in the above article are incorrect. In fact, this appears to be a typo with the SKR manual ([Reference](https://www.reddit.com/r/ender3/comments/wc09uz/bigtreetech_skr_mini_e3_v30_fan_connections/)). Major thanks to [Sharkpoofie](https://www.reddit.com/user/Sharkpoofie/) for providing the following corrections:

      | Header name |	Function | Pin |
      | ----------- | -------- | --- |
      | FAN0 | Part cooling | PC6 |
      | FAN1 | Hot end cooling | PC7 |
      | FAN2 | Electronics enclosure cooling | PB15 |

   Wiring diagram for reference: [SKR Mini e3 V3.0 Wiring Diagram](https://github.com/bigtreetech/BIGTREETECH-SKR-mini-E3/blob/master/hardware/BTT%20SKR%20MINI%20E3%20V3.0/Hardware/BTT%20E3%20SKR%20MINI%20V3.0_PIN.pdf)

4. The hotend does NOT have polarity. You can place the wires in either terminal slot. It is merely a controlled short.
    * [Reference 1](https://www.reddit.com/r/ender3/comments/lx5azz/do_the_hotend_cables_have_polarity_ehy_are_they/)
    * [Reference 2](https://www.reddit.com/r/ender3/comments/bwvdn0/replacing_hot_end_wiring_confusion/)

5. Once you flash Klipper, the Ender 3's LCD screen will go blank. This will be corrected once the printer.cfg file is created.

6. I do NOT recommend using YouMakeTech's printer.cfg file to begin with. It is customized for using a BMG extruder, as well as a BL Touch. Rather, utilize the [printer.cfg](https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/blob/0d290d527142f9daa1aa6f37e96509ac6b961585/configs/Ender3v1_SKR-Mini-e3-V3/printer.cfg) I have created instead.
    * I would recommend using his config for reference if you have these installed, or are thinking about adding them to your machine. 
   
7. I DO recommend using YouMakeTech's [menu.cfg](https://github.com/YouMakeTech/klipper-ender3/blob/8203aa3c9eecd9890e51132bdd0cc69a4b751e18/config/Ender-3%20Pro/SKR-Mini-E3-V3.0/menu.cfg) file. You will simply upload it within Mainsail as a new file. The printer.cfg already uses an "include" statement to reference it.

## Troubleshooting

### Pi Camera and Mainsail OS

This is the best tutorial I have found on this: [Obico - Klipper Webcam Setup using Mainsail](https://www.obico.io/blog/klipper-camera-mainsail/).

Here is a link to my [crowsnest.conf](https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/blob/2801822068c0f1d101cf65081c439dc799d973a2/configs/Ender3v1_SKR-Mini-e3-V3/crowsnest.conf).

## Odds and Ends

### Using BTT Pi

I found [The Feral Engineer's](https://www.youtube.com/watch?v=Ry9Q-toA11w) YouTube tutorial to be very helpful with this. BTT has a specific image that has to be installed on to the BTT Pi. I'm not sure the reason for this, but it is what is referenced in all the other tutorials I looked at regarding this single-board computer (SBC).

There are a few more steps involved with this process, but overall the install is the same as installing Mainsail onto a RPi.

Here are a few more YouTube links that do a great job of explaining how to install Mainsail onto the BTT Pi v1.2:

* [Chris Riley](https://www.youtube.com/watch?v=Df8-7zcwiUc)
* [Stacking Layers](https://www.youtube.com/watch?v=Df8-7zcwiUc&t=2209s&themeRefresh=1)

### Bed Leveling

I figured I'd put a section for this here, as reference. While the Klipper documentation is great, I found these following vids from [PrintsLeo3D](https://youtube.com/@PrintsLeo3D?si=2jvJ5K1J9B70pdCD) to be extremely helpful in this process.

#### No ABL
* [Create a Manual Mesh with Kipper!](https://www.youtube.com/watch?v=yNoPNzFKXvU)

#### ABL
* [BL Touch complete setup for Klipper! Maximize your probed bed mesh!](https://www.youtube.com/watch?v=5vmjBXvY6BA)
* [Accurate BL Touch Offsets](https://www.youtube.com/shorts/FKvPU2nwdts)
* [Let Klipper level your bed with the built-in tool screws_tilt_adjust](https://www.youtube.com/watch?v=APAbl5PGEh0)

<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.


<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

Attributions made in-line with any mentioned references.



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install.svg?style=for-the-badge
[contributors-url]: https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install.svg?style=for-the-badge
[forks-url]: https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/network/members
[stars-shield]: https://img.shields.io/github/stars/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install.svg?style=for-the-badge
[stars-url]: https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/stargazers
[issues-shield]: https://img.shields.io/github/issues/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install.svg?style=for-the-badge
[issues-url]: https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/issues
[license-shield]: https://img.shields.io/github/license/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install.svg?style=for-the-badge
[license-url]: https://github.com/cr45hmurphy/klipper_ender3_skr-mini-e3-v3_install/blob/master/LICENSE.txt
