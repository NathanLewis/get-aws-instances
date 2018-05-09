#!/usr/bin/env python

import os
import sys
import json

if 1 > len(sys.argv):
    print("Usage: getInst.py [-v] <Machine Name> <Json Filename>")
    exit(-1)

verbose = False
argv = sys.argv
if '-v' in sys.argv:
    verbose = True
    argv = [ arg for arg in argv if '-v' != arg ]

name = argv[1]
if 3 == len(argv):
    data = json.load(open(argv[2]))
else:
    data = json.load(open('Instances.json'))


found=False
fuzzy=True # always set to true. Leaving it as a var just in case I want to configure it
for resv in data['Reservations']:
    for inst in resv['Instances']:
        if 'running' == inst['State']['Name']:
            for tag in inst['Tags']:
                #print json.dumps(tag, indent=4, sort_keys=True)
                if ('Name' == tag['Key']) or ('aws:cloudformation:stack-name' == tag['Key']):
                    if ( name == tag['Value']) or ( fuzzy and name in tag['Value']):
                        found=True
                        if verbose:
                            print "%s\t%s\t%s\t%s\t%s" % (inst['PrivateIpAddress'], tag['Value'], inst['LaunchTime'], inst['InstanceId'], inst['ImageId'])
                        else:
                            print inst['PrivateIpAddress']
                        break
                #else if ():
            if found:
                #print inst['PrivateIpAddress']
                found=False
