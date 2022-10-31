# Lab Report

## Less

Less -N
  
      $ less -N plos/pmed.0020048.txt
      1 
      2   
      3     
      4       
      5         
      6         Current journal requirements forcing clinical trials to be registered [1] are
      7         insufficient and are unlikely to solve the problem of negative trials never even making it
      8         to a journal. Most of the patients consenting to clinical trials do so out of altruism. It
      9         is a great betrayal of their trust to suppress clinical trial data. I suggest that
     10         institutional review boards refuse to allow human experimentation unless the protocol is
     11         filed in a central (online) repository. The primary data should also be required to be in
     12         the public domain (say, within 1–2 years after completion). Data obtained by appealing to
     13         altrusitic instincts, similar to money in public charities, are not proprietary
     14         information, nor can physicians cash out the trust of their patients. In reality, it is the
     15         pharmaceutical industry that stands to gain the most if data are made public as such data
     16         inform future research and help smaller, innovative companies avoid redundancy. Voluntarily
     17         sticking to higher standards of ethics will raise societal respect for the industry
     18         (currently being battered for greed) and attract a more talented workforce, and may even
     19         help the current efforts to reform the tort law.
     20       
     21     
     22   
       
Less -N adds line numbers. This is very useful if you want to quickly look inside a file to see where something is.
  
Less -X

    MacBook-Pro-83:technical lukegentry$ less -X plos/pmed.0020048.txt

  
    
      
        
        Current journal requirements forcing clinical trials to be registered [1] are
        insufficient and are unlikely to solve the problem of negative trials never even making it
        to a journal. Most of the patients consenting to clinical trials do so out of altruism. It
        is a great betrayal of their trust to suppress clinical trial data. I suggest that
        institutional review boards refuse to allow human experimentation unless the protocol is
        filed in a central (online) repository. The primary data should also be required to be in
        the public domain (say, within 1–2 years after completion). Data obtained by appealing to
        altrusitic instincts, similar to money in public charities, are not proprietary
        information, nor can physicians cash out the trust of their patients. In reality, it is the
        pharmaceutical industry that stands to gain the most if data are made public as such data
        inform future research and help smaller, innovative companies avoid redundancy. Voluntarily
        sticking to higher standards of ethics will raise societal respect for the industry
        (currently being battered for greed) and attract a more talented workforce, and may even
        help the current efforts to reform the tort law.
      
    
  
    MacBook-Pro-83:technical lukegentry$ 
    
less -X keeps the file in the terminal after quitting. This is useful if you are 
using less to look through a bunch of files and, when you find the right one, you want to keep it in the termiinal.

less -M

    $ less -M plos/pmed.0020050.txt
    
    South Africa [4]). We use data from 51 communities (cities, towns, and villages) in the
        province of KwaZulu–Natal; we exclude communities with a population of less than 500
        people. Data are not available on the number of individuals with HIV in each specific
        community, and thus we use the estimated HIV prevalence in the region (approximately 13% in
    plos/pmed.0020050.txt lines 27-43/384 12%
                                                                               
less -M shows the extra information about the file: the currently displayed lines, the total lines, and the progress.
This would be useful when working with a big file to not get lost.
                                                                               

## Find

-name 

    find . -name chapter*.txt
    ./911report/chapter-13.4.txt
    ./911report/chapter-13.5.txt
    ./911report/chapter-13.1.txt
    ./911report/chapter-13.2.txt
    ./911report/chapter-13.3.txt
    ./911report/chapter-3.txt
    ./911report/chapter-2.txt
    ./911report/chapter-1.txt
    ./911report/chapter-5.txt
    ./911report/chapter-6.txt
    ./911report/chapter-7.txt
    ./911report/chapter-9.txt
    ./911report/chapter-8.txt
    ./911report/chapter-12.txt
    ./911report/chapter-10.txt
    ./911report/chapter-11.txt
   
find -name "name" can be used to list the files with that name. This is very useful when looking for certain files in a database.
                                                                               
-type d

    find . -type d
    .
    ./government
    ./government/About_LSC
    ./government/Env_Prot_Agen
    ./government/Alcohol_Problems
    ./government/Gen_Account_Office
    ./government/Post_Rate_Comm
    ./government/Media
    ./plos
    ./biomed
    ./911report

find -type d lists all the directory and subdirectory names. This is very useful if you want to see what directories there are without being swamped with file names.
                                                                               
fine -iname "name"
                                                                               
    find . -iname Chapter*.txt
    ./911report/chapter-13.4.txt
    ./911report/chapter-13.5.txt
    ./911report/chapter-13.1.txt
    ./911report/chapter-13.2.txt
    ./911report/chapter-13.3.txt
    ./911report/chapter-3.txt
    ./911report/chapter-2.txt
    ./911report/chapter-1.txt
    ./911report/chapter-5.txt
    ./911report/chapter-6.txt
    ./911report/chapter-7.txt
    ./911report/chapter-9.txt
    ./911report/chapter-8.txt
    ./911report/chapter-12.txt
    ./911report/chapter-10.txt
    ./911report/chapter-11.txt
    
 find -iname is like name expcept it is not case sensitive. This is very useful if you are looking for a word in the title but 
 that word could be capatilized in places that you do not know about
 
 ## grep
 
 grep -c
 
    MacBook-Pro-83:technical lukegentry$ grep -c "bio"  ./plos/*.txt
    ./plos/journal.pbio.0020001.txt:5
    ./plos/journal.pbio.0020010.txt:0
    ./plos/journal.pbio.0020012.txt:8
    ./plos/journal.pbio.0020013.txt:2
    ./plos/journal.pbio.0020019.txt:1
    ./plos/journal.pbio.0020028.txt:6
    ./plos/journal.pbio.0020035.txt:13
    ./plos/journal.pbio.0020040.txt:0
    ./plos/journal.pbio.0020042.txt:14
    
grep -c displays the amount of occurences of the pattern in each file. This is very useful for looking to see how many times a pattern appears,
since the normal grep command only displays the file that has the pattern.

grep -l

    lukegentry$ grep -l "chapter"  ./plos/*.txt
    ./plos/journal.pbio.0020010.txt
    ./plos/journal.pbio.0020067.txt
    ./plos/journal.pbio.0020071.txt
    ./plos/journal.pbio.0020112.txt
    ./plos/journal.pbio.0020116.txt
    ./plos/journal.pbio.0020147.txt
    ./plos/journal.pbio.0020187.txt
    ./plos/journal.pbio.0020419.txt
    ./plos/journal.pbio.0020439.txt
    ./plos/journal.pbio.0030062.txt
    
grep -l displays the files with the pattern but not the actual line. This is useful for just finding the files that match the line, not 
clogging it up with the actual file contents.

grep -h

    lukegentry$ grep -h "chapter"  ./plos/*.txt
        Roger Schonfeld ends his very detailed description of JSTOR with a chapter on ‘Lessons
        The Double Helix . The final chapter of his own autobiography addresses
        classic text on evolution (1998) contains 26 chapters totaling 763 pages. To cover the
        topic in only eight chapters and 145 pages, as the Charlesworths have done in 
        his concluding chapters. He emphasises the need to continually review the evidence
        title is not consistent with the knowledge, stated in that chapter, that there is no
        immortality. Hence, this chapter in the report falls short of explaining the serious
        The same chapter offers a sensational quote from a researcher that “the real goal [of
        conclusions are sparse. We guess the aim of the chapter is to illustrate that environmental
        consumption in pensions and health care; most chapters focus on the United States, but the
        closing chapter discusses these issues in a global context. Each essay is followed by a
        Francis is captured in the final chapter of Marr's now classic book “Vision” (Marr 1982).
        or so naturally occurring elements (Shipman et al. 2003; chapter 21 estimates 2,000
        Speciation and the nonmathematical final chapter (“General Conclusions”)
        
grep -h displays only th file contents that match, not the file names. This is useful for looking to see how a pattern pops up, when 
the file name doesn't matter.

