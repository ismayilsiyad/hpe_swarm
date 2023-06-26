HPE-GPG-Signature-Verification-README.txt

https://h20392.www2.hpe.com/portal/swdepot/displayProductInfo.do?productNumber=HPLinuxCodeSigning

-Overview
    The contents of this document will help you verify through GPG, the code you received has been
    signed with digital private keys only held by Hewlett Packard Enterprise Company . In addition
    this ensures that the file has not been manipulated by a third party.

-Download the keys
    Copy the compressed tar file (HPE-GPG-Public-Keys.tar.gz) from the link below to your local
    directory and extract the public keys.
        
        https://downloads.hpe.com/pub/keys/HPE-GPG-Public-Keys.tar.gz

-Verify key used to sign binaries using GPG
    Use the gpg --verify command to find the RSA key ID (ex. 35D00C25) used to sign the binaries.
        # gpg --verify filename.sig filename

-Import the keys for GPG
    For each key that you have identified previously install the public key using the --import flag of the gpg command:
        # gpg --import /path_to_the_key/file_name_of_the_key_ID
        example # gpg --import /path_to_the_key/35D00C25.pub

-Verify using GPG
    Use the gpg --verify command to validate and verify the digital signature of the signed file.
    The output from the command indicates the validity of the signature. Specify the .sig (detached
    signature)file and the corresponding input file in the command:
        # gpg --verify filename.sig filename

    If the level of trust on the key has not been set, you will see a trust level warning similar to this:
        gpg: WARNING: This key is not certified with a trusted signature!
        gpg: There is no indication that the signature belongs to the owner.

    Because you have downloaded the key from this site, and this site is SSL secured by Hewlett
    Packard Enterprise Company, you can ultimately trust that this public key is indeed from Hewlett
    Packard Enterprise Company. Therefore edit the key to set the trust level of the key for proper verification.
    
    First find the "key_name" of the key, type the command below and select the key that you need to trust
        # gpg --list-keys
    
    Example of a "key_name" "Hewlett Packard Enterprise Company RSA 2048 1"
    Edit the key
        # gpg --edit-key "key_name"
    
    Then type the command "trust", and select "5" for trusting the key ultimately. 
    Confirm and type quit to exit 

    Going forward, you should not see the warning about an untrusted identity when verifying the signature.
    Example verification output is below:
        # gpg --verify test.bin.sig test.bin 
        gpg: Signature made Thu 03 Jan 2013 04:48:47 PM UTC using RSA key ID 5CE2D476
        gpg: Good signature from "Hewlett Packard Enterprise Company RSA 2048 1"

