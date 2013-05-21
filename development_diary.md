REPOSITORY URL
=============
https://redmine.ms.mff.cuni.cz/projects/thesis-kaldi-decoder-docs

DEVELOPER DIARY AND REMARKS
===========================

20120918 5
I downloaded some sample data from http://www.repository.voxforge1.org/downloads/SpeechCorpus/Trunk/

20120919 5
Download the rest of voxforge
searching for kaldi tutorials looking at kaldi presentation (docsDropbox/KALDI_description.pdf)

20120922 4
Downloading of DOCS-kaldi.sourceforge.net
running online demo kaldi-trunk/egs/voxforge/online_demo
===============Building kaldi ===============================================
    I am trying to run tutorial in /home/ondra/diplomka/kaldi-trunk/egs/voxforge

    Seams 1-2 OK

    I followed instruction 
    1)for building kaldi-trunk/tools
    2)for building kaldi-trunk/src
    3) following instruction at http://vpanayotov.blogspot.cz/2012/07/voxforge-scripts-for-kaldi.html
       a) downloading data OK
       b) trying to run /home/ondra/diplomka/kaldi-trunk/egs/voxforge/online_demo need to make kaldi-trunk/src/onlinebin than it worked fine 
       c) running s5/run.sh
         have to modify /home/ondra/diplomka/external_voxcforge/extracted/mramige-20100820-thj/wav/a0008.wav

    1)
    CPU throtling problem
    You can not edit files with CPU performance directly /sys/devices/system/cpu/cpu0/cpufreq/cscaling_governor for cpu0 (for cpu1 just replace cpu0)

    I needed to change cpu frequency management
    original set up was ondemand
    I changed it from "ondemand" to "performance via
    sudo cpufreq-set performance   # turns off CPU throtling 

    I installed via
    sudo apt-get install --reinstall libc6-dev
    to solve error 
    /usr/include/features.h:323:26: fatal error: bits/predefs.h


    2)
    in /home/ondra/diplomka/kaldi-trunk/src/configure
    I changed ATLAS/build/install/lib to  ATLAS/build/install/lib
    twice on lines: 168, 235

    NOTE: Do not forget to install fortran compiler (gfortran). Configure fails and the error is a little bit hidden.



    3)a) fixed path - not escaped and path /media/My Book has to be escaped:)
===============end of Building kaldi ========================================

20120923 2
running http://vpanayotov.blogspot.cz/2012/07/voxforge-scripts-for-kaldi.html the tutorial in/home/ondra/diplomka/kaldi-trunk/egs/voxforge/s5
build irstlm5.80.01

20121004-20121009 10
get account ufalssh oplatek@loki.ms.mff.cuni.cz, set it up
get git account  git clone gitolite@redmine.ms.mff.cuni.cz:vystadial.git 
get Redmine account redmine.ms.mff.cuni.cz:vystadial.git
meeting on Thursday 4.10.
reading HTKbook - very slowly first 15 pages

20121014 2
Reading HTK book 

20121015 ?
Set up redmine repo for documentation of my thesis.
Add openfstbc - bash completition for openfst to .bashrc_local
Compiling and running KALDI training on cluster 
    is NOT WORKING and SHOULD BE AVOIDED!:
    -> CPU throtling problem for Atlas libraries
    -> can not disable cpu throtling on every blade on cluster
    -> use loki machine instead -> compilation OK
TODO running http://vpanayotov.blogspot.cz/2012/07/voxforge-scripts-for-kaldi.html the tutorial on cluster /home/ondra/diplomka/kaldi-trunk/egs/voxforge/s5
    -waiting to download voxforge- screen session on lrc2 with interactive login for downloading

20121026
    I should using autoconf, automake, libtool for deploying C code. All available at loki.
    It needs M4 macro preprocessor which is available at loki in enough version 1.4.13

20121016 4
    Installing HTK -> installing srilm & running for cs
        problems on my home machine I needed to install dev-tcl package and I edited common/Makefile.machine.i686  and set up TCL_INCLUDE= -I/usr/include/tcl8.4 and also change tcl to tcl8.4
        still can not find ngram tool
        help found at http://www.speech.sri.com/projects/srilm/manpages/srilm-faq.7.html
        Building srilm ok at T400
    Compiling and running KALDI training on cluster 
        is NOT WORKING and SHOULD BE AVOIDED!:
        -> CPU throtling problem for Atlas libraries
        -> can not disable cpu throtling on every blade on cluster
        -> use loki machine instead
         running http://vpanayotov.blogspot.cz/2012/07/voxforge-scripts-for-kaldi.html the tutorial on cluster /home/ondra/diplomka/kaldi-trunk/egs/voxforge/s5
         not single job despite jobs=1 -> USE RENICE 20!

    Installed HTK -> todo setup config files

20121019 2
    Meeting DRSG -> should use PEP8  -> autopep tools http://pypi.python.org/pypi/autopep8/
    pip install --upgrade autopep8
    PEP8 definition http://www.python.org/dev/peps/pep-0008/

20121015 8
 Set up redmine repo for documentation.
 TODO-compile and run KALDI training na clustru
 running http://vpanayotov.blogspot.cz/2012/07/voxforge-scripts-for-kaldi.html the tutorial on cluster /home/ondra/diplomka/kaldi-trunk/egs/voxforge/s5

20121107
 rewriting notes from the meetings:
 Jan Svec ASR bez LM
 FSM - Finete State Machine
 pjsip C- extension Python
 PIL- Python interpreter lockm runs only 1 thread at one time
 Probabilistic Graphical Models - Daphne Koller (read it)- BP - belief propagation, EP - expected propagation
 GIT - hooks for git - autopep,... postponed
 realtime for ASR == 100ms -> my GOAL
 labeler counts gaussians 
 modes for ending and starting recognition
     PTT - Push to talk
     PTA - Puretone average
 boost python - nice wrapper for C++ even for python 3.x
 use nice, renice commands on loki
 Honza Trmal - contact for ?

 ASR with HTK and Kaldi
    use English data
    monophone->3phone->clustering
    For Kaldi use the same parameters -> use HParam settings from HTK
    I should see error rate around 20%
    HWite look at 2 bigram LM - SLRM-LM tools
 KALDI uses google c++ style guide and I should use cpplint.py
 FINISHED training HTK-scripts except exporting models for Julius ASR
    not used export_models.sh (mkbinhmm & mkbinhmmlist not INSTALLED)

20121109
 Doxygen is not installed on loki / grid but Doxygen 1.7.6.1 is at u-pl21 at mff lab
 tip:   use a cell phone for any presentation with ASR , phones does things for you
        -> noise reduction, volume normalisation ...
 perform KALDI training using nothing special we used for HTK:
  triphone - interword, cepstral mean normalisation, acceleration by mfcc?  
 multipy python -> I have to use the python version for invocation e.g.
    (2.7)ondra@T400$ python2.7 do-my-job.py
 nemam pristup na ssh oplatek@vystadial
 I can use sol11,sol12,sol13
 I copied CUDA-SDK do unlimited cluster, added nvvc to PATH and 
 on twister1 should be GPU for CUDA (It looks like lspci found sthing)
20121111
 SET UP notes: I set up mosh
  HOW I BUILD this for mosh-1.2.3?
  I added ln -s protobufs/include and protbufs/google
  Manually edited genereted makefiles after
  $ protobuf_LIBS='-pthread -lprotobuf -lz -lpthread' protobuf_CFLAGS=-pthread ./configure --prefix=/home/oplatek/tools/mosh-1.2.3/mosh-install
  then I fixed /usr/bin/protoc   -> protobufs/bin/protoc in mosh-1.2.3/src/protobufs/Makefile
  then I fixed LDD_FLAGS in src/frontend makefile
  HOW TO USE MOSH
  http://mosh.mit.edu/#usage

20121114
 HBuild creates a loop for phonems iff I provide
 HBuild phonetic dictionary with "A  phonetic transcription of A\n, B  phonetic transcription of B\n, .." 
 HVite '-p' parameter .... silence threshold, (short words will be occurring instead of silence)
        -p -10 ... less words in sentence -> silence will be occurring more
 Hresult -t parameter shows difference among  the tested transcribed sentence 
 and the recognized transcription of the given sentence
 Htkbook page 51
 HTK Live input
 set sourcerate 1/Sample rate .... in 100ns so 625.0 is for 16 000 sample rate
 HTK can show n-best hypothesis for live input even for incomplete sentences 

 Hmm clustering - phonetic symbol independent -> cluster phonems based on raw vector.

20121115
 Updating and reading /ha/home/oplatek/50GBmax/kaldi/kaldi-trunk/egs/vystadial/s5/run.sh
 Localising changes which hast to be done from voxforge -> vystadial modification
20121123
 ASR with vystadial will get only chunks of wav files and will output chunks of characters.
 Vystadial doc is at https://vystadial.ms.mff.cuni.cz/doc/install.html
 genereted by apidoc and updated by every push to vystadial/doc - git hooks
20120308
  3 month (7-8)*6 hours I have been stuck on really stupid bug: I have kept running on mixed up data in data dir
  Solution is to to clear s5/data directory completely before running a new experiment. (Trying to do simple make function -> really stupid)
  The development of training can be kept by following commit logs in kaldi-vystadial-recipe (on github maybe later will be moved/mirrored on ufal redmine) 
  KALDI status
  
====== current use CUDA ====
source: accessed 20130308 (PSThttp://sourceforge.net/projects/kaldi/forums/forum/1355348/topic/6517393)  
2012-12-24 04:08:35 Nobody:  
I've been trying to apply CUDA to Kaldi and after a while I've grasped that the only place that uses CUDA libraries is nnet/nnetbin that is not used in usual compilation.
So, am I right that CUDA is not used even with -DHAVE_CUDA macro in standart samples?
2012-12-24 13:23:16 PST Dan:
Yes, that is correct.   You can't use CUDA as a drop-in replacement for BLAS operations.  In general the best general purpose option is to compile with multi-threaded MKL.
This is due to inherent limitations in GPU computation-- you have to move data to the GPU card before you can work on it, which must be done "manually", and as a result all computations have to be specially designed for the GPU card (unless you want to do *everything* there, which generally isn't practical).  At some point Intel's Xeon Phi architecture may become more popular, and supported by Kaldi, and that point it may be possible to get GPU-like speedups in a more transparent way.
====== current use CUDA END====

TODO: trying to run  online_decoder /  check out the speed up

compute-wer in local/score.sh compute WER/SER after LM rescoring 
     does NOT compute wer after each iteration of training (I thought it is the case)
     -> TODO compute wer after each iteration or find it out

Real time coeficients 
    produced by gmm-decode-faster which uses gmm-latgen-faster (it logs it)

vyhraneny Diskriminativni model muze byt rychlejsi nez neprorezany model se stejnou wer
Specialized discriminative model could be faster than the uncut model still reaching the same WER value

Idea pro zrychleni primo pro vyhledavani pomoci OpenFST
-dekoder pouziva beam search
-na CPU pouzit uzky search - oznacme ho pruzkumnik
-na GPU hledat pomoci sirsiho search - oznacme ho roj
-TODO - kdy beam search zastavit
- Graf G=(V,E) |V|=n. E=? TODO lze omezit? 
  Necht pruzkumnik ma sirku beamu bP, roj ma sirku bR,
  necht oba prozkoumaji k vrstev posledni vrstva pruzkumnika
  je podmnozinou roje
  TODO
  Pak cas t(pruzkumnik) = O(k*((bP+n)log(bP+n)) hledane n-best list - sortime a
  cas t(roj) = O(
    TODO

KALDI documentation
KALDI - What is exactly rescoring during experiments exp1-4?
    TODO
    We are searching for solutions in alternatives varying parameter "it" from 9 to 20.
    Find where exactly are the parameters of models stored for every single value of "it" 
    TODO 
    Extract the best model over "it" for each setting
    TODO
KALDI - Does the Kaldi framework in my recipe use a special model for OOV words?
        If yes, how to turn it off? 
        TODO
KALDI - In which model does Kaldi use the Language Model (LM) for the first time in the script? (Models appears in increase order of complexity) 
    TODO


/home/oplatek/cuda-samples/0_Simple/matrixMulCUBLAS/matrixMulCUBLAS.cpp

to make online decoder and some other stuff use:
    make ext # from dir /ha/home/oplatek/50GBmax/kaldi/kaldi-trunk/src/

CUDA implementation 
https://code.google.com/p/chmm/
    1) compute the probability of the observation sequence
    2) compute the most probable sequence
    3) train hidden Markov mode parameters

TODO pridat do nejakeho dekoderu simple je vhodny
sbirani statistik kolik se mu vymeni stavu v beamu.


nechat trifonovy model v GPU
a pouzit masku co pridam (vektor |slova| * |pdf|)

language learning - 
skladani modelu rec -> sema
gmm co je?

udelat skript na vyhodnoceni
real time dekoderu
=======
================================
Looking at online decoder
TODO update svn - could use openfst 1.3.3 now I have 1.3.2

I check that portaudio works.
The test
/home/ondra/school/diplomka/kaldi-trunk/tools/portaudio/bin/paex_record
produces reasonable output

online decoder sections:
online-audio-source.h   # uses portaudio
online-cmn.h            # computes cepstral mean normalisation (no variance norm) 
online-faster-decoder.h # TODO
onlinebin-util.h
online-decodable.h
online-feat-input.h     # Computes mfcc/plp (perceptu


GPU MFCC extraction  
    25 * times on CUDA speed up according to P0510_GPUBasedFeature_Extraction_Kou_final_V2.pdf (added to redmine)
    60 * times k-means, EM to 65 times according Azhari.pdf(added to redmine)
    Azhari also implementation of CUDA algorithms
    Use library gpu openblas or how is named
Look at Azhari literature:
 1) N. Kumar, S. Satoor, and I. Buck, "Fast Parallel Expectation Maximization for
 Gaussian Mixture Models on GPUs Using CUDA," in High Performance
 Computing and Communication, 11th IEEE International Conference on, 2009, pp.
 103-109.
 2) Schmadecke, I.; Morschbach, J.; Blume, H.; Inst. of Microeletronic Syst., Leibniz
 Univ., "GPU-based acoustic feature extraction for electronic media processing," in
 Electronic Media Technology (CEMT), 2011 14th ITG Conference on, Dortmund,
 2011, pp. 1-6.
 
 github forked oplatek/pymfcc.py
 another github repo https://github.com/codyaray/speaker-recognition matlab mfcc + speaker recognition

speech_reco_journal_SIPR_20121101_Nov_2012.pdf stress out that mfcc are not the best parameters - look at the other if they are not better for CUDA (probably not)

openfst examples ~/work/openfst   url http://www.openfst.org/twiki/bin/view/FST/FstExamples


======================
ALTERNATIVE DATA for KALDI training available at disks on ufal
======================
New (actually, this time quite old) data published by LDC have arrived. It is a corpus from 1993. If you want it, you can find it on our shared disks (see below).
Jiri Mirovsky
======================

KALDI vystadial-recipe where do I store all parameters for Decoding?
======================
1) Sound input 
    -currently in format of list of files and path to that file stored in input.scp
        input.scp  example
fj228x-001-100517_171607_0001813_0001882 ./data_voip_en/test/fj228x-001-100517_171607_0001813_0001882.wav
2) Model: final.mdl
    usually stored in exp/tri2a/final.mdl
3) HCLG.fst (model-infst-in)
    usually stored in exp/tri2a/graph/HCLG.fst
4) words.txt (word-symbol-table): 
    usually stored in exp/tri2a/graph/words.txt
5) silence-phones (stored nowhere - passed directly as parameter)
    typically first 5 phones labels e.g.
    '1:2:3:4:5'
6) FILE where to stored DEDOCED OUTPUT:
    ark,t:exp-decode/trans.txt
7) FILE where to stored DEDOCED ALIGNMENT:
    ark,t:exp-decode/ali.txt
8) OTHER numeric parameters e.g.: 
    online-wav-gmm-decode-faster --verbose=1 --rt-min=0.8 --rt-max=0.85 --max-active=4000 --beam=12.0 --acoustic-scale=0.0769

20130408 Fixed computing wer in decode-online.sh however 
============================================================================
File: fj228x-001-100518_171600_0001776_0001887 (failing on this or the next file)
PUB

NO

ERROR (online-wav-gmm-decode-faster:Compute():feature-mfcc.cc:80) Mfcc::Compute, no frames fit in file (#samples is 256)
ERROR (online-wav-gmm-decode-faster:Compute():feature-mfcc.cc:80) Mfcc::Compute, no frames fit in file (#samples is 256)

[stack trace: ]
kaldi::KaldiGetStackTrace()
kaldi::KaldiErrorMessage::~KaldiErrorMessage()
kaldi::Mfcc::Compute(kaldi::VectorBase<float> const&, float, kaldi::Matrix<float>*, kaldi::Vector<float>*)
kaldi::OnlineFeInput<kaldi::OnlineVectorSource, kaldi::Mfcc>::Compute(kaldi::Matrix<float>*, unsigned int*)
kaldi::OnlineCmvnInput::Compute(kaldi::Matrix<float>*, unsigned int*)
.
.
.
kaldi::FasterDecoder::ProcessEmitting(kaldi::DecodableInterface*, int)
kaldi::OnlineFasterDecoder::Decode(kaldi::DecodableInterface*)
online-wav-gmm-decode-faster(main+0x11df) [0x5bd263]
/lib/libc.so.6(__libc_start_main+0xfd) [0x7f0653803c4d]
online-wav-gmm-decode-faster() [0x5bbfc9]

============================================================================

For decoding using gmm-latgen-faster + lattice-best-path 
to generate lattice and find the best path in the lattice  
gmm-latgen-faster

============================================================================
MFCC_Z_A_D What does it mean in Kaldi?

HTK vs KALDI compatability now fixed everything suggested


HTK settings for MFCC vs // nynejsi nastaveni Kaldi
TARGETKIND = MFCC_0_D_A_Z    // delta a accelerated delta OK, Mean substraction YES per Speaker 
TARGETRATE = 100000.0          // stejne  shifted by 10ms each time
WINDOWSIZE = 250000.0         // stejne 25ms
USEHAMMING = T                   // vypnuto da se zapnout
PREEMCOEF = 0.97                // stejne
NUMCHANS = 26                     // stejne NUMCHANS requires an integer value specifying the number of filter-bank channels to use in the analysis
CEPLIFTER = 22                      // stejne
NUMCEPS = 12                       // 13 ale stejny vyznam
ENORMALISE = T                    // Nedela se
ZMEANSOURCE = T                // zapnuto 
USEPOWER = T                       // 
LOFREQ = 125                          // nyni 20
HIFREQ = 3800                          // nyni Nyquist 8000



Zakladni nastaveni pouzite ted v Kaldi:
(Ziskane prikazem $ /net/work/people/oplatek/kaldi/kaldi-trunk/src/featbin/compute-mfcc-feats --help)
--frame-length               : Frame length in milliseconds (float, default = 25)
--frame-shift               : Frame shift in milliseconds (float, default = 10)

--num-ceps                  : Number of cepstra in MFCC computation (including C0) (int, default = 13)
--num-mel-bins              : Number of triangular mel-frequency bins (int, default = 23)

--low-freq                  : Low cutoff frequency for mel bins (float, default = 20)
--high-freq                 : High cutoff frequency for mel bins (if <= 0, offset from Nyquist) (float, default = 0)

--cepstral-lifter           : Constant that controls scaling of MFCCs (float, default = 22)

V recipe byla zmenena nasledujici optiona zmenena na FALSE
 --use-energy                : Use energy (not C0) in MFCC computation (bool, default = true)
============================================================================


How to interface Kaldi to Python?
1)Kaldi Code 
2)C very thin wrapper around C++ code See:
http://www.parashift.com/c++-faq-lite/mixing-c-and-cpp.html
3) C-Python wrapper around C thin wrapper of C++. See 
http://cffi.readthedocs.org/en/latest/

Why not swig etc? Because C is very well testable wrapper of its own.
And the cffi looks very transparent. Everyone who knows C/C++ can read it.
=======

Decoding with lattices
======================
In decode/decode-lattice.sh I am using gmm-latgen-faster
I have to use the best acwt value for the final decoder


Length of in test data_voip_en1 computed:
$ for f in /ha/home/oplatek/50GBmax/kaldi-trunk/egs/kaldi-vystadial-recipe/s5/data_voip_en1/test/*.wav ; do soxi -D $f ; done | awk '{s+=$1} END {print s}'
2465.98 # in seconds

Time measure decode/decode-lattice.sh
======================
Measuring 1
==========
make_mfcc.sh
real    0m55.400s
user    0m52.211s
sys     0m0.200s
compute_cmvn_stats.sh 
real    0m0.278s
user    0m0.152s
sys     0m0.056s
gmm-latgen-faster
real    34m2.767s   2042.767s
user    33m57.723s  2037.723s
sys     0m1.484s

total time decoding:   
real    2098.4
user    2090.1
sys     1.74

Measuring 2
==========

make_mfcc.sh
  real    0m57.313s
  user    0m51.115s
  sys     0m0.392s
compute_cmvn_stats.sh 
  real    0m0.222s
  user    0m0.152s
  sys     0m0.056s
gmm-latgen-faster
  real    41m22.908s
  user    41m18.875s
  sys     0m2.668s
lattice-best-path
  real    0m1.306s
  user    0m1.172s
  sys     0m0.080s




Interfacing Kaldi from Python
=============================
UPDATE: It is necessary to build the shared library with *gcc*! 
Cffi is slow from Python fast from Cython.
Is intended as better c_types.

Cffi needs shared library! 
So I have to rebuild all object files with -fPIC flag!
I changed the main Makefile in kaldi-trunk/src directory - just added -fPIC to cxx_flags.

I need to checkout gmm-online-decoder for generating the mfcc features
frame by frame.

Use pyaudio to test Kaldi cffi interface -> DO TESTS!

TODO look at vystadial - how is ASR interfaced?


Building atlas, lapack
---------------------
On sol11 I was able to build new static atlas library
TODO how to create shared library

$ pwd
/ha/work/people/oplatek/kaldi-trunk/tools/ATLAS
$ mkdir build && cd build
$ ../configure --shared --incdir=/ha/work/people/oplatek/kaldi-trunk/tools/atlas_install_dir # needed specified the target dir too
# running make with 
$ EXTRA_CXXFLAGS=-fPIC make  # see kaldi.mk where is the EXTRA_CXXFLAGS variable used


How I build Kaldi? ./configure generate kaldi.mk -> I need to add fPIC 
    add fPIC to python-mfcc/Makefile: EXTRA_CXXFLAGS ?
TODO: how to modify .configure to generate libtools.so libfeats.so etc?
    or should I do it in python-mfcc/Makefile (and similar makefiles) ? probably yes/no?


The experiment 6 from commit aa7263b3f5c151409a87e3d845d58e39335a4f0c finished.
Problem extracting data. Maybe sthing missing



-----------------------------------
for working with Python extension I need everything like shared library
to build openfst like shared library
I ran from kaldi-trunk/tools/openfst-1.3.2 directory
mkdir ../openfst-1.3.2_install
# we need shared libraries for python integration, kaldi needs static for its linking
./configure --enable-shared --enable-static --prefix=`pwd`/../openfst-1.3.2_install


Launching Vystadial
--------------------
 * I needed to create checkout vystadial-private to alex/resources and rename it to alex/resources/private.
 * alex/resources/default.cfg stores all the main configs
 * Configs can be applied on top of each other. They are dictionaries and new values to keys are assign as new config is read. So the last one can overwrite the previous one
 * From vystadial/alex/applications I run webhub.py
    * Before that I needed to create aio_call_log where it stores the same audio which is submitted
 * After running webhub.py there is webserver running by default at http://localhost:8000. 
 * I HAVE TO SPECIFY the directory where my wavfiles are located by 
    going to url and type 
    `http://localhost:8000/?dir=source_wavs`
    if I created directory `alex/applications/source_wavs`
 * Then you can click on one of the wavs displayed by the webpage or
 put a similar line at your urlbar :
 `http://localhost:8000/?dir=source_wavs&play=source_wavs/jurcic-001-120912_134200_0001993_0002036.wav`
 * At kronos/loki/sol launched the website on localhost and use lync (press g) and paste  
    `http://localhost:8000/?dir=source_wavs`