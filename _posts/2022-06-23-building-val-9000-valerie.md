## Building VAL-9000 (Valerie)
The 90s definitely had a more analogue feel for computing. 56K modems were dreams of jacking into the Matrix. Floppy disk drives etched precious data onto the magnetised discs like a mason committing hieroglyphs to stone, and with just as much noise. When the decibels humming from the beige PC towers would grow louder, you knew the monolithic machine was thinking.
On weekends, my father would sometimes take me to the office to pick up important documents, and while he'd sort through his desk and in-trays, I'd use the chance to mess around with MS Paint on his Windows 98 machine. VGA colours were astounding to me at the time.
In the early 2000s, my parents bought me my first computer from a little shop in a Cairo mall. It was powered by a Pentium 4 with a whopping 30GB of SATA HDD space and 1GB of RAM. It ran Windows XP with skies of blue and fields of green splashed across the background - it really was 'Bliss'.
The Egyptian man who built it for me made sure to fill My Videos with Bollywood films so that we wouldn't have to buy as many VCDs. He even installed Resident Evil 3 (never played it at that age on account of having a weak bladder).
I loved that machine.
I hacked it and learned everything I could about computing along the way - and that meant a lifelong love for programming.
I only started earning real money recently. With that first paycheck I built VAL 9000 (Valerie). Kubrick and Clarke would have been proud of my progress since the simian past.
Valerie would be the first PC I'd build myself from start to finish purely for the purpose of being a Machine Learning Workstation.
Coming out of the whole process, I've come to appreciate just how standardised and user-friendly modern computing hardware and PC-building has become. There's a lot of information out there on compatibility and build guides, which are a far cry from the world of the early 2000s when I last chose my desktop build after reading magazines.
> "Then the first explorers of Earth, recognising the limitations of their minds and bodies, passed on their knowledge to the great machines they had created, and who now transcended them in every way." - 2001: A Space Odyssey
I needed to build something more haunting than the darkest abysses weighing in the depths of my lizard brain. I needed to build something indicative of my first forays in artificial intelligence. Something that could evolve to subsume me both metaphorically & literally. Valerie's hardware capabilities needed to be ready for the intelligence that could transcend my own pathetic sentience. I have a mouth and I must scream.
Valerie needed to run Linux.
Why? Because:
```bash
sudo dnf install cmatrix -y
cmatrix
```
But also because Linux comes with the latest version of Python 3 out of the box. Linux makes it easy to start building Machine Learning models right away, without resorting to aliases or messing with symlinks on Windows, hunting online and downloading Python IDLE just for the interpreter, followed by installing a bunch of IDEs to manage your packages and environments.
I picked Fedora Linux for a few reasons:
1. It's free and open source
2. GNOME experience is responsive and consistent and best on Fedora
3. Stable, secure, versatile, and frequently updated
4. Compilers, interpreters, IDEs, and programming tools are built-in / easily accessible
5. Wide selection of software available with DNF on RPM repository
6. Latest software available through Flatpak and Snaps
7. No bloat

Fedora is a pretty clean and fully-featured distro. While Ubuntu would have been an equally good choice for the fantastic software and driver compatibility, I went with Fedora because new technologies are deployed sooner and there is no Amazon spyware. Using it makes me want to tinker like I did in my halcyon days of Windows XP.
The only downside of Fedora I would add are the slow speeds of DNF due to all the metadata it downloads compared to APT on Debian-based distros. The upside of this is DNF's stability from its delta package download system.
Generally I use the following tools:
1. Python 3
2. gcc-g++
3. R Studio
4. GNU/Octave
5. Visual Studio Code (RPM from Microsoft)
6. Jupyter Lab

Handling large datasets necessitates significant memory availability, fast read/write speeds from disk, and CPU-based processing power. The amount of RAM would need to be high and with low latency (at most CL-16).
Juggling large datasets in memory, performing transformations, and then writing back to disk are some of the operations which may be necessary, and having the sufficient RAM to fulfill overhead becomes critical. For these reasons, the core components I chose were:
- 2 x 8GB G.Skill Ripjaws V DDR4 SDRAM @ 3.2GHz (CL-16–18–18–38)
- AMD Ryzen 7 3700X CPU w/ 8-Core 16-Thread @ 3.6GHz
- Samsung 980 PRO PCIe 4.0 NVMe M.2 SSD 500GB

That Ryzen 7 takes on a workload and the RAM is no-nonsense no-gamer RGB, perfectly compatible with the upper bound for the CPU.
When building more complex things like artificial neural networks and deep learning models, libraries like Keras and Tensorflow leverage GPU processing power. Even if you are (and should be) relying on cloud computing, it's still a good idea to have sufficient GPU power to test your model locally first. For the GPU I chose:
- MSI NVIDIA GeForce RTX 2060 Ventus OC w/ 6GB GDDR6 VRAM @ 1710MHz
- Corsair RM 650W 80 PLUS Gold Certified Fully Modular PSU

Valerie isn't as great for deep learning. I've yet to pop in a second GPU for it, and I'm sure I'll need to swap out the PSU for 750W as well to account for the power draw of a RTX 3090 or similar. Using multiple NVIDIA GPUs benefit from CUDA cores and VRAM needed in deep learning.
I've got a project lined up that will use the YOLOv3 algorithm implemented in C, and I'll keep track of dataset size and model training times to measure Valerie's performance for posterity.
To fit all that onto a motherboard, I went with the MSI MPG X570 Gaming Pro Carbon WiFi Motherboard. Note, the motherboard choice limits me to 2 parallel GPUs only.
To fit that motherboard into an ATX case as monolithic, imposing, and exuding eldritch sentience as HAL 9000's red eye, I picked the Fractal Design Meshify 2 ATX Black. I believe Fractal are based in Sweden where personalities can be equally cool and distant as their climes.
The stock Ryzen cooling fan can be lit up to an ominous red. It adds just the right atmosphere to Valerie reading your lips in that upcoming Computer Vision to Text implementation.
