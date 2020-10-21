# ta2-pipeline

## external edl_data
http://159.89.180.81/demo/resources/edl_data.tar.gz

-----------------------------------------------------------
## For system developer
### docker-compose version
Please use version 3

e.g.,
```
version: "3"
```

### Control startup order
To control the startup order, please detect if a `_success` file has been generated from the previous container at the beginning of your code. For example,


    # Control startup order in docker-compose
    if os.path.exists('%s/_success' % outdir):
        msg = 'A successful file already exists in the current output dir, exit'
        logger.info(msg)
        exit(0)
    # Check successful file from previous component
    success_file_path = '%s/_success' % '/'.join(pnam.split('/')[:-1])
    s = time.time()
    while not os.path.exists(success_file_path):
        logger.info('edl has been waiting for: %.3f seconds' % (time.time()-s))
        time.sleep(15)
    # os.remove(success_file_path)
    logger.info('start...')


And generate a `_success` at the end of your code.
For example,

    with open('%s/_success' % output_dir, 'w') as fw:
        fw.write('')
