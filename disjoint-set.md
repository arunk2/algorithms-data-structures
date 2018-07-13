
    class disjoint_set(object):
        def __init__(self):
            self.partitions_count = 0
            self.forest = {}
            self.parent = {}

        def make_set(self, element):
            if not self.find(element):
                new_partition = partition(element)
                self.parent[element] = element
                self.forest[new_partition.representative] = new_partition
                self.partitions_count += 1

    def union(self, x, y):
        if x != y:
            if self.forest[x].size < self.forest[y].size:
                self.forest[y].add(self.forest[x].show())
                #Update parent details 
                self.parent[self.forest[x].representative] = self.forest[y].representative
                self.delete(x)
            else:
                self.forest[x].add(self.forest[y].show())
                #Update parent details 
                self.parent[self.forest[y].representative] = self.forest[x].representative
                self.delete(y)

    def find(self, element):
        if self.parent[element] == element:
            return element
        else:
            return find(element)
