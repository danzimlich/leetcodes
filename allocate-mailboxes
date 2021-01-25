""""
https://leetcode.com/problems/allocate-mailboxes
Python3
Dan Zimlich
""""

import random
class Solution:
    def minDistance(self, houses: List[int], k: int) -> int:
        
        # Sort houses.  Extra cost but can get rid of this later.  This is the easiest way for a decent initialization (I think)
        houses.sort()  #cost is O(n log n)
        
        #### If k = 1, just return the median ####
        if k == 1:
            if len(houses) % 1:
                median = houses[int(len(houses)/2)]
            else:
                median_hi = houses[int(len(houses)/2)]
                median_lo = houses[int(len(houses)/2)-1]
                median = int((median_hi + median_lo)/2)
            #print("median: ",median)
            
            min_dist = 0
            for h in range(0, len(houses)):
                min_dist = min_dist + abs(median - houses[h])
            #print("min_dist: ", min_dist)
            return min_dist
                           
        
        #### 1-D K-means cluster ####
        best_cost = 10000**2 #start arbitrarily large
        best_mailbox_locs = [1] * k
            
        # initialize clusters evenly
        #mailbox_loc_init_dist = len(houses) / (k+1)

        #mailbox_locs = []  ###### THESE ARE THE CENTROIDS #####

        #for i in range (0, k):
        #    mbx_loc = int(mailbox_loc_init_dist * (i+1))
        #    mailbox_locs.append(houses[mbx_loc])
            #print("mailbox locations ", mailbox_locs)
            
        
            
        #print("mailbox_locs before K-MEANS: ", mailbox_locs)
        for iter_of_random_init in range(0, 100):
        ######## K-MEANS with ONE random centroid initialization #######
            #### psuedo-random mailbox_loc inits ####
            mailbox_locs = []  ###### THESE ARE THE CENTROIDS #####
            for mbx in range(0, k):
                mailbox_locs.append(random.randint(houses[0],houses[len(houses)-1]))
            #print("mailbox_locs before K-MEANS iter #",iter_of_random_init,": ", mailbox_locs)

            # initialize mailbox_for_house list (takes vals btw 1 to k)
            mailbox_for_house = [0] * len(houses)
            #print("mailbox_for_house init ", mailbox_for_house)

            ########### K-MEANS ALG: ASSIGN mailboxes (centroids) / MOVE mailboxes ################# 
            for k_iter in range(0, 10):
                
                # ASSIGN one of k mailboxes to each house
                for i in range (0, len(houses)):
                    shortest_dist = 10001**2  #expensive memory?
                    #Arbitrary large number, there are only 10^4 possible addresses
                    for mailbox in range (0, k):
                        ##cheaper than sqrt of euclid norm?
                        dist = (houses[i] - mailbox_locs[mailbox])**2  
                        if (dist < shortest_dist):
                            shortest_dist = dist;
                            mailbox_for_house[i] = mailbox;
                #print(mailbox_for_house)

                # MOVE mailboxes: Compute means based on centroid assignments
                
                #print("mailbox for house ", mailbox_for_house)
                for mailbox in range (0, k):
                    sum_mb = 0
                    count = 0
                    for h in range(0, len(mailbox_for_house)):
                        if (mailbox_for_house[h] == mailbox):
                            sum_mb = sum_mb + houses[h]
                            count = count + 1
                    #print("sum ", sum_mb, " count ", count)
                    if count != 0:
                        mean = sum_mb / count
                        mailbox_locs[mailbox] = mean
                
                #print("new mailbox locs ", mailbox_locs)
                k_iter = k_iter + 1
            

            #print("new mailbox locs ", mailbox_locs)

            # set mailbox_locs to integers
            for mailbox in range(0, k):
                mailbox_locs[mailbox] = int(round(mailbox_locs[mailbox]))
                #mailbox_locs[mailbox] = int(mailbox_locs[mailbox])
            #print("new mailbox loc ints ", mailbox_locs)
            
            # compute the final answer
            min_total_dist = 0
            for h in range(0, len(houses)):
                min_total_dist = min_total_dist + abs(houses[h] - mailbox_locs[mailbox_for_house[h]])
            #print("min_total_dist: ", min_total_dist)
            #print("mailbox locs: ", mailbox_locs)
            #print("mailbox_for_house ", mailbox_for_house)
            #return(min_total_dist)
            
            if min_total_dist < best_cost:
                best_cost = min_total_dist
                best_mailbox_locs = mailbox_locs
            
            ################ END OF ONE random init of K-MEANS ##############
            iter_of_random_init = iter_of_random_init + 1

        #print("best_mailbox_locs: ", best_mailbox_locs)
        #print("best_cost: ", best_cost)
        return(best_cost)
            
