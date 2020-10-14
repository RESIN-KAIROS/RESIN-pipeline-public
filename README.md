# ta2-pipeline

## test input data
https://drive.google.com/file/d/1Qi_ahiZfDGKO3VCvWMiYdENp7o6w_-B_/view?usp=sharing

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


    success_file_path = '%s/_success' % input_dir
    s = time.time()
    while not os.path.exists(success_file_path):
        logger.info('foo has been waiting for: %.3f seconds' % (time.time()-s))
        time.sleep(15)
    os.remove(success_file_path)
    logger.info('start...')

And generate a `_success` at the end of your code.
For example,

    with open('%s/_success' % output_dir, 'w') as fw:
        fw.write('')
