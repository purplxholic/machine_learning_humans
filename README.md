# machine_learning_humans

how viterbi works:
'''
    huge_transition = {(START,O):0.,(START,B-postive):0.,...} 
    huge_emission = {(WORD,TAG):0...,} : emission is TAG -> WORD
    td = ['Hello','Bob','#UNK#']
    #forward 
    tags = ['O','B-postive','B-negative','B-neutral','I-positive','I-negative','I-neutral']
    
    v = for tag in tags 
    where k = 1,...,n 
    recursive case:
    
    find all the values going towards (k,v)
    
    eg for node y2 for word "WE"
    
    calculate all the pi values of possible combinations of states 
    eg O -> B+ for the word "WE", O-> O for the word "WE", O-> B- for the word "WE", etc 
    for k in range(1,len(ONE SENTENCE)): TODO: do some check to seperate STOP,START sequence 
        eg y2 
        for v in tags:
            #in each y2's states 
            for u in tags:
                #test y2 state against all of y1's states 
                if emission[("WE",v)] * transition[(u,v)] are not in the dicts:
                    emission[("WE",v)] = 0 , transition[(u,v)]=0 <- whichever 

                one_pi = all pi(k-1,v) * emission[("WE",v)] * transition[(u,v)]
                #eg y2 = "O", y1 = "B-postiive", y2 = "O", y1 = "B-neutral"  , ETC 
                temp pi(k,v)[u] = one_pi <- insert all values
                #eg y2 = "O", y1 = "B-postiive" is inserted as "B-postiive" : 0.03 

            max_pi_k_v[v] = max(temp pi(k,v)) <- use the weird max from dictionary fucntion to select the best score 
            #eg for v = "O" , found that pi is max at 0.5 for u="I-neutral" among the different u for y2
            #register as "O" : 0.5 (so found one score for one v)
            
        since we have finished finding the max pi(k,v) for y2, add to the dict all pi(k,v)
        all pi(k,v)[k] = max_pi_k_v
        

    temp pi(k,v) dictionary =
    {'B-POSITIVE':0.1,
     'B-NEGATIVE':0.2,
     ...
    }
    max_pi_k_v = 
    {'O':0.5,
    'B-positive':0.9,
    ...}
    
    
    create dictionary all pi(k,v)
    = {1:
        {
        'B-POSITIVE':0.1,
        'B-NEGATIVE':0.2,
        ...}
        
        }
    where the key is k/current node value  
    '''