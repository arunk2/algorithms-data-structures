## Extract Nouns:
It is important to extract nouns and related adjective words from a sentences.

### Working code:
```
import re, nltk, sys
from nltk.corpus import stopwords

NOUNS = ['NN', 'NNS', 'NNP', 'NNPS']
ADJ = ['JJ', 'JJR', 'JJS']

stopwords_en = set(stopwords.words('english'))

def extractEntities(text):
		entities = []
		# Remove all the unicode characters before processing
		text = re.sub(r'[^\x00-\x7F]+',' ', text)
		for sent in nltk.sent_tokenize(text):
			for chunk in nltk.ne_chunk(nltk.pos_tag(nltk.word_tokenize(sent)), binary=True):
				
				if hasattr(chunk, 'label'):
					for c in chunk.leaves():
						if c[1] in NOUNS or c[1] in ADJ:
							#print chunk
							#print c
							if c[0].lower() not in stopwords_en:
								entities.append(c[0].lower())
				else:
					if chunk[1] in NOUNS or chunk[1] in ADJ:
						#print chunk
						if chunk[0].lower() not in stopwords_en:
							entities.append(chunk[0].lower())

		if len(entities) > 0:
			return ' '.join(entities)
		else:
			return ''

if __name__ == "__main__":
	if len(sys.argv) == 2:
		print extractEntities(sys.argv[1])
	else:
		print 'Exception: could not find message for parsing. Usage: python extract.py "<<<MESSAGE>>>"'
```
