def grabYamls():
   yamls = []
   #Grab the current dir
   currentdir = os.path.dirname(__file__)
   #Get relative path for atomic test descriptions
   atomic_red_dir = os.path.join(currentdir, 'atomic-red-team', 'atomics')

   #Grab all the yamls
   for root, subdirs, files in os.walk(atomic_red_dir):
      for filename in files:
         file_path = os.path.join(root, filename)
         if ".yaml" in file_path:
            yamls.append(file_path)

   return yamls

def yamlsToDataFrame(yaml_list):
    tdf = pd.DataFrame()
    for atomic_yaml in yaml_list:
        with open(atomic_yaml, 'r') as atomic_set:
            yamld = yaml.safe_load(atomic_set)
            if 'atomic_tests' in yamld.keys():
                YamlDF = pd.json_normalize(yamld,record_path='atomic_tests',meta=['attack_technique','display_name'])
            tdf = pd.concat([YamlDF,tdf])
    return tdf


tests = grabYamls()
j = yamlsToDataFrame(tests)
j['platforms'] = j['supported_platforms'].apply(lambda x: ','.join(str(y) for y in x))
