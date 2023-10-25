class Solution:
    def visiblePoints(self, points: List[List[int]], angle: int, location: List[int]) -> int:
        
        if len(points)==1:
            return 1
 
        from math import pi, atan
 
        # выражение угла в радианах
        angle = angle*pi/180
 
        # нормализация всех точек
        i, j = location[0], location[1]
        for k in range(len(points)):
            x, y = points[k]
            points[k] = [x-i, y-j]
 
        # выражение всех точек в радианах
        temp = []
        for k in range(len(points)):
            x, y = points[k]
            if x!=0 or y!=0:
                if x>0:
                    if y>=0:
                        temp.append(atan(y/x))
                    else:
                        temp.append(2*pi+atan(y/x))
                elif x==0:
                    if y>0:
                        temp.append(pi/2)
                    else:
                        temp.append(3*pi/2)
                elif x<0:
                    temp.append(pi+atan(y/x))
 
        temp.sort()
        
        duplicate = []
        for k in range(len(temp)):
            duplicate.append(temp[k]+2*pi)
        temp.extend(duplicate)
 
        maxnum = 0
        i, j = 0, 0
        while j<len(temp):
            if temp[j]-temp[i] <= angle:
                maxnum = max(maxnum, j-i+1)
                j+=1
            else:
                if i==j:
                    j+=1
                else:
                    i+=1
 
        return maxnum + points.count([0,0])
