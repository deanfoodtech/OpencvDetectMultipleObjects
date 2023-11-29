import cv2 as cv
import numpy as np

#read the file using opencv
forest_img = cv.imread('forest.png', cv.IMREAD_UNCHANGED)
tree_img = cv.imread('tree1.png', cv.IMREAD_UNCHANGED)

#converting all picture to cv-readable format
tree_imgs = []
for png in ['tree1.png', 'tree2.png', 'tree3.png']:
    tree_imgs.append(cv.imread(png, cv.IMREAD_UNCHANGED))
#matching
result = cv.matchTemplate(forest_img, tree_img, cv.TM_CCOEFF_NORMED)

results = []#contains matches
tree_images = ['tree1.png', 'tree2.png', 'tree3.png']
for imgs in tree_imgs:
    results.append(cv.matchTemplate(forest_img, imgs, cv.TM_CCOEFF_NORMED))
#now we need to get the best match position
#print(results)
#I want to get all max_loc from the results
max_locs = []
for member in results:
    min_val, max_val, min_loc, max_loc = cv.minMaxLoc(member)
    max_locs.append(max_loc)
print(max_locs)


min_val, max_val, min_loc, max_loc = cv.minMaxLoc(result)
# print(cv.minMaxLoc(result))
# print(tree_img.shape)
threshold = 0.8
(w,h,c) = tree_img.shape
print(w)
#.shape will give a tuple of 3 - width, height, channels
# top_left = max_loc
# bottom_right = (max_loc[0]+h, max_loc[1]+w)

if max_val >= threshold:
    print('found the target at'+str(max_loc))
    tree_w = tree_img.shape[1]
    tree_h = tree_img.shape[0]
    # print(str(tree_w) + "is the same as w:" + str(w))

    # top_left = max_loc
    # bottom_right = (top_left[0]+tree_w, top_left[1]+tree_h)
    for locs in max_locs:
        top_left = locs
        bottom_right = (top_left[0]+tree_w, top_left[1]+tree_h)
        cv.rectangle(forest_img, top_left, bottom_right,
                 color=(0,255,0), thickness=2, lineType=cv.LINE_4)
    cv.imshow('TM_CCOEFF_NORMED', forest_img)
    cv.waitKey()
else:
    print('target not found')
