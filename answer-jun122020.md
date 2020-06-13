# 21.1 请简述`open`函数具有哪些行参（parameter),各个行参（parameter)什么含义，分别代表什么功能。

答：`open`函数的行参有：file,mode,buffering,encoding,errors,newline,closefd,opener。

file is either a text or byte  string giving the name (and the path if the file isn't in the current working directory) of the file to be opened or an integer gile descriptor of the file to be wrapped. (If a file descriptor is given,it is closed when the returned I/O object is closed,unless closefd is set to False.)

mode is an optional string that specifies the mode in which the file is opened. It defaults to 'r' which means open for reading in text mode.Other common values are 'w' for writing (truncating the file if it already exists),'x' for creating and writing to a new file, and 'a' for appending (which on some Unix systems,means that all writes append to the end of the file regardless of the current seek position).In text mode,if encoding is not specified the encoding used is platform dependent:locale.getpreferredencoding(False) is called to get the current locale encoding.(For reading and writing raw bytes use binary mode and leave encoding unspecified.)The available modes are:

=========================================================================

## Character Meaning

-------------------------------------------------------------------------
- 'r'  open for reading(default)
- 'w'  open for writing,truncating the file first
- 'x'  create a new file and open it for writing 
- 'a'  open for writing,appending to the end of the file if it exists
- 'b'  binary mode
- 't'  text mode(default)
- '+'  open a disk file for updating (reading and writing)
- 'U'  universal newline mode (deprecated)

=========================================================================

The default mode is 'rt'(open for reading text).For binary random access,the mode 'w+b' opens and truncates the file to 0 bytes,while 'r+b' opens the file without truncation.The 'x' mode implies 'w' and raises an `FileExistsError` if the file already exists.

Python distinguishes between files opened in binary and text modes,
even when the underlying operating system doesn't. Files opened in
binary mode (appending 'b' to the mode argument) return contents as
bytes objects without any decoding. In text mode (the default, or when
't' is appended to the mode argument), the contents of the file are
returned as strings, the bytes having been first decoded using a
platform-dependent encoding or using the specified encoding if given.
    
'U' mode is deprecated and will raise an exception in future versions
of Python.  It has no effect in Python 3.  Use newline to control
universal newlines mode.

buffering is an optional integer used to set the buffering policy.
    Pass 0 to switch buffering off (only allowed in binary mode), 1 to select
    line buffering (only usable in text mode), and an integer > 1 to indicate
    the size of a fixed-size chunk buffer.  When no buffering argument is
    given, the default buffering policy works as follows:
    
    * Binary files are buffered in fixed-size chunks; the size of the buffer
      is chosen using a heuristic trying to determine the underlying device's
      "block size" and falling back on `io.DEFAULT_BUFFER_SIZE`.
      On many systems, the buffer will typically be 4096 or 8192 bytes long.
    
    * "Interactive" text files (files for which isatty() returns True)
      use line buffering.  Other text files use the policy described above
      for binary files.
    
encoding is the name of the encoding used to decode or encode the
    file. This should only be used in text mode. The default encoding is
    platform dependent, but any encoding supported by Python can be
    passed.  See the codecs module for the list of supported encodings.

errors is an optional string that specifies how encoding errors are to
    be handled---this argument should not be used in binary mode. Pass
    'strict' to raise a ValueError exception if there is an encoding error
    (the default of None has the same effect), or pass 'ignore' to ignore
    errors. (Note that ignoring encoding errors can lead to data loss.)
    See the documentation for codecs.register or run 'help(codecs.Codec)'
    for a list of the permitted encoding error strings.
    
newline controls how universal newlines works (it only applies to text
    mode). It can be None, '', '\n', '\r', and '\r\n'.  It works as
    follows:
    
    * On input, if newline is None, universal newlines mode is
      enabled. Lines in the input can end in '\n', '\r', or '\r\n', and
      these are translated into '\n' before being returned to the
      caller. If it is '', universal newline mode is enabled, but line
      endings are returned to the caller untranslated. If it has any of
      the other legal values, input lines are only terminated by the given
      string, and the line ending is returned to the caller untranslated.
    
    * On output, if newline is None, any '\n' characters written are
      translated to the system default line separator, os.linesep. If
      newline is '' or '\n', no translation takes place. If newline is any
      of the other legal values, any '\n' characters written are translated
      to the given string.

If closefd is False, the underlying file descriptor will be kept open
    when the file is closed. This does not work when a file name is given
    and must be True in that case.
    
A custom opener can be used by passing a callable as *opener*. The
    underlying file descriptor for the file object is then obtained by
    calling *opener* with (*file*, *flags*). *opener* must return an open
    file descriptor (passing os.open as *opener* results in functionality
    similar to passing None).
    
open() returns a file object whose type depends on the mode, and
    through which the standard file operations such as reading and writing
    are performed. When open() is used to open a file in a text mode ('w',
    'r', 'wt', 'rt', etc.), it returns a TextIOWrapper. When used to open
    a file in a binary mode, the returned class varies: in read binary
    mode, it returns a BufferedReader; in write binary and append binary
    modes, it returns a BufferedWriter, and in read/write mode, it returns
    a BufferedRandom.
    
It is also possible to use a string or bytearray as a file for both
    reading and writing. For strings StringIO can be used like a file
    opened in a text mode, and for bytes a BytesIO can be used like a file
    opened in a binary mode.

# 21.2 请简述 `open` 函数支持哪些模式 (mode),并讨论他们之间的区别。 
答：`open`函数支持以下8种模式：

- 'r'  open for reading(default)
- 'w'  open for writing,truncating the file first
- 'x'  create a new file and open it for writing 
- 'a'  open for writing,appending to the end of the file if it exists
- 'b'  binary mode
- 't'  text mode(default)
- '+'  open a disk file for updating (reading and writing)
- 'U'  universal newline mode (deprecated)


The default mode is 'rt'(open for reading text).For binary random access,the mode 'w+b' opens and truncates the file to 0 bytes,while 'r+b' opens the file without truncation.The 'x' mode implies 'w' and raises an `FileExistsError` if the file already exists.

Python distinguishes between files opened in binary and text modes,
even when the underlying operating system doesn't. Files opened in
binary mode (appending 'b' to the mode argument) return contents as
bytes objects without any decoding. In text mode (the default, or when
't' is appended to the mode argument), the contents of the file are
returned as strings, the bytes having been first decoded using a
platform-dependent encoding or using the specified encoding if given.
    
'U' mode is deprecated and will raise an exception in future versions
of Python.  It has no effect in Python 3.  Use newline to control
universal newlines mode.

# 21.3 请写代码,打开并读取 `os` 模块的源代码,并将其显示在终端上。
答：

# 21.4 如何理解文件对象 (file object) 和磁盘文件 (disk file) 之间的关系?我们为什么要手动关闭文件对象?
答：文件 (file) 位于 磁盘 (disk),Python 需要根据文件 (file) 处于文件系统 (file system) 的路径 (path),在
内存 中创建出一个指向该路径 (path) 的对象 (object),借此对象 (object) 的 read 和 write 方法
(method) 来完成对磁盘文件的读写 (I/O) 操作 (operation)。

磁盘文件是一种资源,Python 进程需要向操作系统申请 ( open ) 并成功才能获得,使用完毕之后需要
手动 释放 ( close )。Python 解释器 (interpreter) 虽然有 垃圾回收 (garbage collection, GC) 功能,但
回收的仅限于内存对象 (object),并不包括像文件 (file) 这样的外部资源。Python 解释器 (interpreter)
进程 (process) 虽然在退出时会释放所有已申请但尚未释放的资源,但还是建议 Python 程序员自己,
在使用完毕后及时释放资源,以免资源被过久占用,从而影响其他进程 (process) 运行。

# 21.5 请写代码,以写入 (write) 为例,演示文件缓存 (buffer) 的概念,即演示 “写入文件” 与 “写入磁盘” 的区别。
答：文件对象 (file object) 是在 内存 而并不是在 磁盘。调用 write 方法只是改变文件对象 (file
object) 所持有的 缓存 (buffer),并不必然 写入到磁盘。只有在缓存 (buffer) 满后,文件对象 (file
object) 才会 自动 向操作系统申请写入磁盘,并清空缓存 (buffer)。设立缓存 (buffer) 的目的是减少 I/O
调用次数,因为磁盘 (disk) 读写的速度相对于内存 (memory) 读写的速度而言要慢许多倍 (约几十倍)。
若要 手动 将缓存 (buffer) 写入磁盘并清空,可以调用文件对象 (file object) 的 flush 方法 ( close 方
法在关闭文件对象之前,其实会自动调用 flush 方法)。

```
>>>f = open('file.txt','w') #打开一个可写的文件对象。
>>>f.write('hi')  #将'hi'写入文件缓存，但是未写入磁盘。
>>>f.close() #调用 f 对象的 close 方法,关闭文件,缓存在文件对象内的文本内容此时才真正写入磁盘
```

# 21.6 请写代码,以读取 (read) 为例,演示文件位置 (position) 的概念,包括获取当前位置、移动当前位置等操作。
答：用文件对象 (file object) 的 tell 方法可以获取当前位置 (position),用 seek 方法可以移动位置 (position) 至指定的字节数。

```
$cat file.txt 
你好这是我的abcdefg
$python3
>>>f = open('file.txt','r')
>>>f.tell()  # 获取当前位置
0
>>>f.read(3)  #读取3个字符
'你好这'
>>>f.tell()  #每个中文字符占用3个字节，每个英文字母占用1个字节
9
>>>f.seek(3) #移动位置至第4个字节
>>>f.read()
'好这是我的abcdefg'
```
# 21.7 请写代码,以编码(encoding)的概念为基础,演示读/写文本(text)文件与读/写二进制(binary)的等价操作。
答：
```
>>>f2 = open('file2.txt','w')
>>>f2.write('我爱学习')
>>>f2.close()
$cat file2.txt
我爱学习
>>>f2 = open('file2.txt','rb')
>>>content = f2.read()
>>>content
b'\xe6\x88\x91\xe7\x88\xb1\xe5\xad\xa6\xe4\xb9\xa0'
>>>f2.close()
>>>f3 = open('file3.txt','wb')
>>>f3.write(content)
>>>f3.close()
$cat file3.txt
我爱学习 
```
# 21.8 请写代码,演示通用换行符 (universal newline) 的概念,包括打开和关闭该功能,以及读写之间的差异。先演示写入,再演示读取。
答：
```
>>>f4 = open('file4.txt',mode='w') #默认开启通用换行符功能
>>>f4.write('a\r\nb\nc\rd')
8
>>>f4.close()
>>>f4 = open('file4.txt',mode='r',newline='')
>>>f4.read()
'a\r\nb\nc\rd'
>>>f4.close()
>>>f4 = open('file4.txt',mode='r')
>>>f4.read()  # '\r\n','\r'全部转化为'\n'
'a\nb\nc\nd'
>>>f4.close()

>>>f5 = open('file5.txt',mode='w',newline='') #关闭通用换行符功能
>>>f5.write('a\r\nb\nc\rd')
>>>f5.close()
>>>f5 = open('file5.txt',mode='r',newline='')
>>>f5.read()
'a\r\nb\nc\rd'
>>>f5.close()
>>>f5 = open('file5.txt',mode='r')
>>>f5.read()
'a\nb\nc\nd'
>>>f5.close()
```

# 21.9 请写 Python 代码,获取当前工作目录,再把当前工作目录切换至文件系统根目录,再把当前目录切换至用户根目录。
答：
```
>>>import os 
>>> os.getcwd() # 获取当前工作目录
'/home/zzx/Projects/answers'
>>> os.chdir('/') # 切换至文件系统根目录
>>> os.getcwd()
'/'
>>> os.chdir('/home/zzx') # 切换至用户根目录
>>> os.getcwd()
'/home/zzx'
```
# 21.10 请写 Python 代码,展示 /etc 目录下的内容 (目录和文件),并判断该目录下的 profile 名称是目录还是文件。
答：
```
>>> import os
>>> os.listdir('/etc')
['crontab', 'lsb-release', 'gtk-3.0', 'vim', 'ssl', 'update-manager', 'lighttpd', 'udev', 'pnm2ppa.conf', 'cups', 'vtrgb', 'update-motd.d', 'bindresvport.blacklist', 'bash_completion.d', 'PackageKit', 'wpa_supplicant', 'gtk-2.0', 'netplan', 'gshadow', 'cron.d', 'v2rayL', 'ldap', 'sane.d', 'zsh_command_not_found', 'issue.net', 'hosts', 'insserv.conf.d', 'login.defs', 'mke2fs.conf', 'locale.alias', 'cron.hourly', 'os-release', 'pki', 'vdpau_wrapper.cfg', 'modules-load.d', 'dconf', 'perl', 'rpc', 'networks', 'apparmor.d', 'mime.types', 'rc0.d', 'sslocal.json', 'deluser.conf', 'rc5.d', 'timezone', 'ca-certificates.conf', '.pwd.lock', 'locale.gen', 'rc4.d', 'skel', 'gshadow-', 'tmpfiles.d', 'subgid-', 'pulse', 'newt', 'fonts', 'magic', 'mtab', 'pm', 'calendar', 'libreoffice', 'services', 'rc2.d', 'inputrc', 'acpi', 'ufw', 'brltty.conf', 'host.conf', 'avahi', 'apg.conf', 'ld.so.cache', 'appstream.conf', 'python3', 'environment', 'apport', 'ld.so.conf.d', 'networkd-dispatcher', 'pam.conf', 'sysctl.conf', 'binfmt.d', 'securetty', 'udisks2', 'mailcap', 'dnsmasq.conf', 'sudoers.d', 'grub.d', 'resolvconf', 'python2.7', 'console-setup', 'printcap', 'terminfo', 'hostname', 'proxychains.conf', 'hostid', 'anacrontab', 'apache2', 'rarfiles.lst', 'rcS.d', 'fuse.conf', 'ifplugd', 'libblockdev', 'popularity-contest.conf', 'modprobe.d', 'vconsole.conf', 'libaudit.conf', 'bash_completion', 'brltty', 'speech-dispatcher', 'X11', 'python3.7', 'dhcp', 'kernel', 'pcmcia', 'adduser.conf', 'geoclue', 'usb_modeswitch.d', 'sudoers', 'manpath.config', 'rc.local', 'protocols', 'ssh', 'rc1.d', 'apt', 'libao.conf', 'ImageMagick-6', 'group-', 'passwd-', 'shadow', 'debconf.conf', 'bluetooth', 'group', 'cracklib', 'hp', 'environment.d', 'opt', 'alternatives', 'default', 'magic.mime', 'kerneloops.conf', 'fstab', 'ppp', 'shadow-', 'rc6.d', 'mysql', 'groff', 'thunderbird', 'emacs', 'rmt', 'hosts.deny', 'ubuntu-advantage', 'firefox', 'init', 'ltrace.conf', 'chromium-browser', 'rsyslog.d', 'sysctl.d', 'papersize', 'apm', 'openvpn', 'rc3.d', 'bash.bashrc', 'resolv.conf', 'dpkg', 'iproute2', 'gai.conf', 'passwd', 'snmp', 'kernel-img.conf', 'logrotate.conf', 'ca-certificates', 'apparmor', 'initramfs-tools', 'whoopsie', 'legal', 'logrotate.d', 'fprintd.conf', 'mtools.conf', 'depmod.d', 'chatscripts', 'rsyslog.conf', 'gconf', 'security', 'alsa', 'init.d', 'ucf.conf', 'polkit-1', 'cron.weekly', 'cron.monthly', 'UPower', 'nsswitch.conf', 'gss', 'xdg', 'vulkan', 'subuid', 'libpaper.d', 'sensors.d', 'v2ray', 'cupshelpers', 'brlapi.key', 'e2scrub.conf', 'dictionaries-common', 'usb_modeswitch.conf', 'gdm3', 'pam.d', 'ghostscript', 'polipo', 'ld.so.conf', 'logcheck', 'modules', 'mailcap.order', 'libnl-3', 'nanorc', 'xattr.conf', 'thermald', 'issue', 'subuid-', 'machine-id', 'wgetrc', 'network', 'hdparm.conf', 'selinux', 'NetworkManager', 'gnome', 'systemd', 'subgid', 'mecabrc', 'cron.daily', 'profile.d', 'update-notifier', 'dbus-1', 'localtime', 'fwupd', 'gdb', 'hosts.allow', 'rygel.conf', 'shells', 'debian_version', 'sensors3.conf', 'python', 'profile', 'glvnd']
>>> os.path.isfile('/etc/profile')
True
```

# 21.11 请写 Python 代码,在当前目录下新建一个 week15 目录,在week15目录下新建一个名为temp.py的文本文件,向其中写入文本 print('Hello World!') ,然后将其删除。
答：
```
>>> import os,pathlib
>>> p = pathlib.Path('week15')
>>> p.mkdir()
>>> fp = p / 'temp.py'
>>> f = fp.open('w')
>>> f.write("print('Hello World!')")
21
>>> f.close()
>>> os.remove('week15/temp.py') #删除temp.py
```

# 21.12 请写 Python 代码,计算 datetime 模块的源代码的目录名、文件名和扩展名,并在此基础上获取其所在目录下的其他目录名和文件名。
答：
```
>>> import os,datetime
>>> p = datetime.__file__
>>> p
'/usr/lib/python3.7/datetime.py'
(path,filename) = os.path.split(p)
>>> path
'/usr/lib/python3.7'
>>> filename
'datetime.py'
>>> ext = os.path.splitext(filename)[1]
>>> os.listdir(path)
['_bootlocale.py', 'xdrlib.py', 'zipfile.py', 'pdb.py', '_compat_pickle.py', 'rlcompleter.py', 'urllib', 'uuid.py', 'modulefinder.py', 'trace.py', 'abc.py', '_sysconfigdata_m_linux_x86_64-linux-gnu.py', 'csv.py', 'cmd.py', 'tabnanny.py', 'tty.py', 'cProfile.py', 'types.py', 'logging', 'random.py', 'numbers.py', 'glob.py', 'keyword.py', 'lib2to3', 'socketserver.py', 'dummy_threading.py', 'sysconfig.py', 'py_compile.py', 'mailcap.py', 'calendar.py', '__future__.py', 'netrc.py', 'imaplib.py', '_threading_local.py', 'pickle.py', 'symtable.py', 'plistlib.py', 'filecmp.py', 'compileall.py', 'aifc.py', 'fnmatch.py', '_dummy_thread.py', 'io.py', 'timeit.py', 'sitecustomize.py', 'weakref.py', 'reprlib.py', 'base64.py', 'pty.py', 'socket.py', 'LICENSE.txt', '_compression.py', 'gzip.py', 'warnings.py', 'bdb.py', 'pydoc_data', 'enum.py', 'traceback.py', 'stringprep.py', 'html', 'locale.py', 'heapq.py', 'os.py', 'distutils', 'decimal.py', 'sqlite3', 'asynchat.py', 'shutil.py', 'encodings', 'stat.py', 'lib-dynload', 'telnetlib.py', 'ntpath.py', 'bisect.py', 'smtpd.py', 'pprint.py', 'ensurepip', 'contextlib.py', 'json', 'tempfile.py', 'optparse.py', 'concurrent', 'genericpath.py', 'textwrap.py', 'site.py', 'subprocess.py', 'code.py', 'smtplib.py', 'profile.py', 'webbrowser.py', 'antigravity.py', 'difflib.py', 'turtle.py', '_weakrefset.py', 'secrets.py', 'mailbox.py', 'poplib.py', '_pyio.py', 'formatter.py', 'nturl2path.py', 'venv', 'dataclasses.py', '_osx_support.py', 'hmac.py', 'runpy.py', 'cgitb.py', 'fractions.py', '_sitebuiltins.py', 'copyreg.py', '_collections_abc.py', 'operator.py', '_pydecimal.py', 'pickletools.py', 'collections', 'signal.py', 'email', 'mimetypes.py', 'shlex.py', 'getopt.py', 'imghdr.py', 'pipes.py', 'macpath.py', 'pstats.py', 'argparse.py', 'ssl.py', 'functools.py', 'linecache.py', 'sre_constants.py', 'platform.py', 'sched.py', 'colorsys.py', 'lzma.py', 'curses', 'inspect.py', 'test', 'tokenize.py', 'fileinput.py', 'xml', 'queue.py', 'codeop.py', 'posixpath.py', 'wsgiref', '_py_abc.py', 'typing.py', 'quopri.py', 'tarfile.py', 'asyncore.py', 'ast.py', 'ctypes', 'bz2.py', 'getpass.py', 'configparser.py', 'struct.py', 'sre_parse.py', 'token.py', 'this.py', 'statistics.py', 'ftplib.py', 'sre_compile.py', '_strptime.py', 'crypt.py', 'pyclbr.py', 'zipapp.py', 'ipaddress.py', 'pathlib.py', 'string.py', 'threading.py', 'shelve.py', '__phello__.foo.py', '__pycache__', 're.py', 'dbm', 'doctest.py', 'pydoc.py', 'symbol.py', 'importlib', 'multiprocessing', 'sunau.py', 'copy.py', 'pkgutil.py', 'asyncio', 'binhex.py', 'nntplib.py', 'uu.py', 'http', 'wave.py', 'tracemalloc.py', 'unittest', 'hashlib.py', '_markupbase.py', 'opcode.py', 'dis.py', 'imp.py', 'config-3.7m-x86_64-linux-gnu', 'cgi.py', 'sndhdr.py', 'gettext.py', 'xmlrpc', 'contextvars.py', 'selectors.py', 'codecs.py', 'chunk.py', 'datetime.py']
```

# 请写 Python 代码,使用路径对象 (path object),用一条语句创建出目录./week06/lecture01/trash ,并在其下创建 greeting.exe 文件,在其内部写入字符串 '无效命令' 用 'utf-16' 编码得出的二进制字节串。
答：
```
>>> import pathlib
>>> p = pathlib.Path('./week06/lecture01/trash')
>>> p.mkdir(parents=True,exist_ok=True)
>>> fp = p / 'greeting.exe'
>>> fp.write_text("无效命令",encoding='utf-16')
4
>>> p1 = pathlib.Path('./week06/lecture01/trash/greeting.exe')
>>> f = open(p1,'rb')
>>> content = str(f.read())
>>> content
b'\xff\xfe\xe0eHe}T\xe4N'
>>> f.close()
>>> f = open(p,'w')
>>> f.write(content)
25
>>> f.close()
```
