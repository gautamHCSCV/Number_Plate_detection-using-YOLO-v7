## Results on images in exp folder:

![image](https://user-images.githubusercontent.com/65457437/192200650-859bd490-4f78-4faa-a08c-5d6ac514d3c3.png)

## Algorithm: (overlapping bounding boxes)

def overlap_bbox(bbox1, bbox2):
    
    xc1,yc1,w1,h1 = bbox1
    xc2,yc2,w2,h2 = bbox2

    if xc2+w2/2<xc1-w1/2 or xc2-w2/2>xc1+w1/2:
        return 0
    if yc2+h2/2<yc1-h1/2 or yc2+h2/2<yc1-h1/2:
        return 0
    return 1
    
    
def detect_three_people(predictions):
    
    detections = [a[0] if a[1]==' ' else '-1' for a in predictions]
    
    n_bikes = detections.count('3')
    n_human = detections.count('0')
    if n_bikes==0 or n_human<3:
        return []

    bike,people = [],[]

    for i in range(len(detections)):
        predictions[i].replace('\n','')
        if detections[i]=='3':
            bike.append(list(map(float,predictions[i][2:].split(' '))))
        elif detections[i]=='0':
            people.append(list(map(float,predictions[i][2:].split(' '))))
    
    results = []

    for bbox1 in bike:
        cnt = 0
        for bbox2 in people:
            if overlap_bbox(bbox1, bbox2) or overlap_bbox(bbox2, bbox1):
                cnt+=1
            if cnt>=3: 
                results.append(bbox1)
                continue

    #print(results)
    return results
    
    
    
path = 'runs/detect/exp/labels/'

#print(os.listdir(path))

for ff in os.listdir(path):

    with open(path+ff) as f:
    
        predictions = f.readlines()
        result = detect_three_people(predictions)
        
        if len(result)>0:
            print('More than 2 people on a motorbike detected in',ff)
        else:
            print('No harm detected in', ff)
