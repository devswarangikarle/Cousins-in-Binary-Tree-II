# Cousins-in-Binary-Tree-II

Given the root of a binary tree, replace the value of each node in the tree with the sum of all its cousins' values.
Two nodes of a binary tree are cousins if they have the same depth with different parents.
Return the root of the modified tree.
Note that the depth of a node is the number of edges in the path from the root node to it.

from collections import deque
class Solution:
    def replaceValueInTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        
        pq = deque()
        pq.append((root.val, root))
        
        while pq:
            n = len(pq)
            
            levelSum = 0
            for localSum, node in pq:
                levelSum += node.val
                
            for i in range(n):
                localSum, node = pq.popleft()                
                childSum = 0
                if node.left: childSum += node.left.val
                if node.right: childSum += node.right.val                
                if node.left: pq.append((childSum, node.left))
                if node.right: pq.append((childSum, node.right))
                   
                node.val = levelSum - localSum
                 
        return root
