#LAMMA   (BETA)


###Vulnerability Assessment Framework for all the Crypto Implimentations.


(An Open Source Initiative by - SECURITY MONX )




Lamma Framework Documentation  (beta)

        File Name   :   README

        Author      :   @ajithatti

        Org         :   Security Monx

        Version     :   0.0.1

        Purpose		: 	Gives introduction of Lamma Framework (beta)




Table Of Contents   :

        A.      Licenses Information
        B.      Introduction to Lamma Framework (beta)
        C.      Dependencies
        D.      Using LAMMA
        E.      Features
        F.      Note
        G.      Contributors




A. Licenses Information

    LAMMA Framework (beta) and its documents are covered with NO Licenses.
    You are free to use it in any way you want. No conditions what so ever.

    For details about the project visit our website
        "http://www.securitymonx.com/Project-LAMMA"




B. Introduction to LAMMA Framework (beta)

    LAMMA Framework  (beta) aims to be a comprehensive suite for
    auditing cryptography, PKI and related implementations.

        LAMMA (beta) supports 4 major modules

            REMOTE
            CRYPTO
            TRUST
            SOURCE

1.  REMOTE - Module scans remote Hosts for SSL/TLS configuration, and reports any gap, vulnerabilities discovered.

            Primary Checks :
            a)  SSL/TLS version, session management & server configurable parameters
            c)  Checks for use of vulnerable/depricated cipher suites
            b)  Server certificate Test
                    Verification Type (EV/OV/DV)
                    Time line analysis of applicable SSL/TLS vulnerabilities
                    Verification, validation
                    Information Leaks
                    Common Modulus
                    Signature algorithm strength
                    Alternate Names

2.  CRYPTO -    This Module checks the various crypto primitives generated by
                any underlying framework for Quality, backdoor & sanity. Few of

            Primary Checks :
                Quality Test for Random Number Generated
                Sanity Checks for shared Prime numbers in multiple RSA keys
                Safe and Strong Prime test
                Shared modulus test
                MalSha, Malformed Digest Test


3.  TRUST -     Module checks various trust and key stores for - insecure Private
                keys and untrusted certificates.

            Primary Checks:
            a)  Private Keys
                    Stored with/without encryption
                    Access permission
                    Track multiple instances
                    Extract Prime for CRYPTO Module test

            b)  Public Key
                    Extract Modulus for CRYPTO Module test
                    Track multiple instances


            b)  Certificates
                    Check in trutsted store & CRL
                    List pinned & untrusted certificate
                    Track multiple instances
                    Verification, Time line analysis common with REMOTE Module

4.  SOURCE - Module is primalry to enforce "Cryptography Review Board" recommendations
            of your organisation. This module scans source code for use of insecure and
            depricated cryptographic schemes.

            a)  Depricated Schemes
                    MD Family hashing schemes
                    SHA/SHA1 hashes
                    ECB/CBC block cipher mode
                    rand() or /dev/rand functions
                    <More Depricated/Insecure Schemes>

            b) Weak Schemes (Backdoored Schemes)
                    Dual_EC_DRBG
                    prime2566v1
                    p224r1
                    secp384r1
                    < More weaker/backdoored schemes





C. Dependencies  :   LAMMA needs few Python packes for its functioning. List of the packages required are :

                    1.  cmd2  - Runs the custom shell of Lamma

                         pip install cmd2

                    2.  subprocess - Invoke Openssl or other scripts

                        pip install subprocess

                    3.  pyOpenSSL - Wrapper over OpenSSL

                        pip install openssl





D. Using LAMMA   :

1.  LAMMA.py kicks off the framework, with a welcome screen and leads to LAMMA prompt

            $> python LAMMA.py
                                         __    _____ _____ _____ _____
                                        |  |  |  _  |     |     |  _  |
                                        |  |__|     | | | | | | |     |
                                        |_____|__|__|_|_|_|_|_|_|__|__|

                                                    (BETA)


                                Vulnerability Assessment and Auditing Framework
                                      for all the Crypto Implementations.


                                           (An Open Source Project)

                                                      by

                                                SECURITY MONX




            LAMMA :


2. You can view micro help on each of the module using "help module" command

            LAMMA : help trust
                  Scans a given trust/key stored for -  untrusted certs, insecure private keys,


            LAMMA : help source
              Scans the source code for known weak or backdoored functions


            LAMMA : help crypto
              Generate keys, hashes, random number under various schemes for a given counts


            LAMMA : help remote
              Scans the remote host and reports the SSL/TLS configuration profile & applicable vulnerabilities


            LAMMA :



3.  To know how tu use each of the module, simply type the module name and you will get elaborate usage help.


            LAMMA : remote

            remote [-H] [-s] [-l] [-o] [-i] [-p] [-h]

            Purpose  : Scan a remote host with given plugin over SSL/TLS connection


                -H [--help]      : prints this usage help
                -s [--script]    : scan the target with given script id or 'all','gen',  or 'reg'
                -l [--list]      : list all the plugins and plugin IDs
                -o [--out]       : reports are stored in this file else default file
                -i [--in]        : input file name with multiple IP:Port specified in each line
                -p [--port]      : port on which SSL or TLS connection is to be made
                -h [--host]      : IP or Domain name of the remote host to be connected

            LAMMA :



4.  Sample usage of "remote" module, We are scanning "null.co.in" for plugins in gen are results will be stored in final.html file.


            LAMMA : remote -h null.co.in -p 443 -s gen -o final.html


            [*]  Lamma Scanning Service [Started] ...


            [+]  Parametrs set for this Scan :

                 Tests to Run => gen     Target Host =>  null.co.in
                 Target port =>  443
                 Reports will be stored in file => final.html


            [+] Starting the scan

             Kick gen


            [+] Kick Starting... /home/evader/Desktop/RELEASE/LAMMA/modules/remote-module/gen


                Now Executing:   server_config.py  -h null.co.in -p 443 -o final.html
                Now Executing:   scan_ssl.py  -h null.co.in -p 443 -o final.html

            [+] Scanning complete...

            LAMMA :

5. Output of the "remote" scanning module for "null.co.in"

            --- Starting Server Config Checks for host - null.co.in ---

            Server Response :

            HTTP/1.1 500 Internal Server Error
            Server: nginx
            Date: Fri, 03 Jun 2016 18:05:58 GMT
            Content-Type: text/html
            Connection: close
            X-Powered-By: PHP/5.5.9-1ubuntu4.16


            Certificate Chain validation :

             Cert of  Digital Signature Trust Co. :	is Valid
             Cert of  Let's Encrypt :	is Valid
             Cert of  null.co.in :	is Valid
             Certificate Chain is verified & Trustable

            --- Server Configuration checks Complete...

            --- Scanning host  started ---


            Remote Host name :null.co.in
            Remote Host IPv4 :104.237.152.34
            Remote Host Port :443
            Cipher Suite used : ECDHE-RSA-AES128-GCM-SHA256
            Subject Name = null.co.in
            Issuer Name = Let's Encrypt Authority X1
            Start Date : 20160313112800Z
            End Date   : 20160611112800Z
            Signature Algorithm : sha256WithRSAEncryption
            subjectAltName:
                jobs.null.co.in
                 null.co.in
                 www.null.co.in
            [INFO] The Certificates Verification type : DV
            Public Key Size [2048]

            --- End of the SSL Scan ---





E.     Features    :

The LAMMA project is a work in progress. We are along with many functional features we are trying to stick to these basic principles :

        1.  Simple      :   User need not have deep understanding of cryptography
                        to use this framework. It should be intutive and simple to
                        use with minimu learning.

        2.  Extensible  :    The framework should be extensible. User community should
                        be able to extend the functionalities easily by adding custom
                        plugins.

        3.  Indipendent :   The framework itself uses OpenSSL & python wrappers over it
                        but can be used to test the Cryptography, PKI & related
                        implementations, independent of the technology used like (Java,
                        NSS, GnuTLS, SChannel )to engineer them.

        4.  Automation  :   "Large scale assessment of the crpto-implementation, with
                        ease" is our prime focus behind the design of this framework





F.    Note    :

    a.  LAMMA(beta) is living project.
    b.  Currently it is build for Linux platform
    c.  Code is provided with all the rights and bugs to you without any guarantee or responsibility
        from the author
    d.  We welcome bugs, comments, criticsms, contributions or even a simple note on your experience
        with LAMMA (beta). Write to us at

            a j i t [ a t ] s e c u r i t y m o n x [ d o t ] c o m






G.Contributors

    1.  Ajit Hatti - @ajithatti <twitter handle>
