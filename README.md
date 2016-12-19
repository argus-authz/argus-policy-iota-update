# argus-policy-iota-update
Update script for Argus policy files to adapt them for use with IOTA CAs.

## description
The Argus PAP simplified policy defines blocks of permit and deny rules. Within
EGI, only certain VOs are permitted to use certificates published by IOTA CAs,
and this needs to be reflected in the permit rules. In practice this means that
rule matching a VO or FQAN type attribute, need to be accompanied by a rule
matching the name of the corresponding policy. For convenience the Argus PAP
comes with two 'meta' policy info files called `policy-aspen-birch-cedar.info`
and `policy-aspen-birch-cedar-dogwood.info` providing the overall policy for
either standard VOs or VOs allowed to use IOTA CAs.

This tool can automatically update the existing Argus PAP simplified policy to
implement or update (in case the list of VOs has changed) the permit rules
concerning this additional matching rule. Lines containing the policy-name
attribute with a different value from one of the two special values are left
untouched.

## usage
Obtain the current policy from the Argus PAP, e.g.:

    pap-admin lp > policies_20161219.orig
    
Run the tool:

    argus-policy-iota-update policies_20161219.orig policies_20161219.new
    
Update the policies in the Argus PAP:

    pap-admin rap && pap-admin apf policies_20161219.new
