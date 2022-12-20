<h2>Info:</h2>
<h3>Firmware Reversing Steps</h3>
<p>
  The firmware is first obtained from the vendor's website or extracted from the device to perform the analysis<br>
  The obtained/extracted firmware, usually a binary file, is first analysed to figure out its type (bare metal or OS based).<br>
  It is verified that the firmware is either encrypted or packed. The encrypted firmware is more challenging to analyse as it usually needs a tricky workaround, such as 
  reversing the previous non-encrypted releases of the firmware or performing hardware attacks like Side Channel Attacks (SCA) to fetch the encryption keys.<br>
  Once the encrypted firmware is decrypted, different techniques and tools are used to perform reverse engineering based on type.
</p>
<h2>Static Analysis</h2>
<h3>Binwalk</h3>
<p>
  Extraction tool. Extracts code snippets inside any binary by searching for signatures against many standard binary file formats like <b>zip, tar, exe, ELF,</b> etc.<br>
  Binwalk has a database of <b>binary header signatures</b> against which the signature match is performed.<br>
  The common objective of using this tool is to extract a file system like <b> Squashfs, yaffs2, Cramfs, ext*fs, jffs2,</b> etc., which is embedded in the firmware binary.<br>
  <ul><li><i>binwalk -E -N</i></li></ul>
  <ul><li>https://github.com/ReFirmLabs/binwalk</li></ul>
</p>
<h3>FMK Firmware ModKit</h3>
<p>
  It extracts the firmware using binwalk and outputs a directory with the firmware file system.<br>
  Once the code is extracted, a developer can modify desired files and repack the binary file with a single command. <br>
  <ul><li><i>extract-firmware.sh</i></li></ul>
  <ul><li>https://www.kali.org/tools/firmware-mod-kit/</li></ul>
</p>
<h3>FirmWalker</h3>
<p>
  Searches through the extracted firmware file system for unique strings and directories like <b>etc/shadow, etc/passwd, etc/ssl,</b><br>
  special keywords like <b>admin, root, password,</b> etc.,vulnerable binaries like <b>ssh, telnet, netcat</b> etc.
  <ul><li>https://github.com/craigz28/firmwalker</li></ul>
</p>
<h2>Dynamic Analysis</h2>
<h3>Qemu</h3>
<p>
  Free and open-source emulator and enables working on cross-platform environments.<br>
  provides various ways to emulate binary firmware for different architectures like Advanced RISC Machines (ARM), Microprocessors without Interlocked Pipelined Stages (MIPS), etc., on the host system.<br>
  Qemu can help in full-system emulation or a single binary emulation of ELF (Executable and Linkable Format) files for the Linux system and many different platforms.
  <ul><li>https://www.qemu.org/</li></ul>
</p>
<h3>Gnu DeBugger (GDB)</h3>
<p>
  Dynamic debugging tool for emulating a binary and inspecting its memory and registers.<br>
  GDB also supports remote debugging, commonly used during firmware reversing when the target binary runs on a separate host and reversing is carried out from a different host.
  <ul><li>https://www.sourceware.org/gdb/</li></ul>
</p>
