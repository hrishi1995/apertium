#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <libxml/HTMLparser.h>

char *inline_tags[] = {"i", "u", "b"};

int i_tag = sizeof(inline_tags)/sizeof(inline_tags[0]);

char *block_tags[] = {"div", "p", "h1", "h2", "h3", "h4", "h5", "h6"};

int b_tag = sizeof(block_tags)/sizeof(block_tags[0]);



void apert_format(xmlNode * a_node)
{
	xmlNode *cur_node = NULL;
	int flag=0,i=0;

	int max_len;

	if(i_tag>b_tag)
	{
		max_len=i_tag;
	}
	else
	{
		max_len=b_tag;
	}    	

	if(NULL == a_node)
	{
        	return;
    	}

	for (cur_node = a_node; cur_node; cur_node = cur_node->next) 
    	{
        	if (cur_node->type == XML_ELEMENT_NODE) 
        	{
			
			for(i = 0; i <3; ++i)
			{
    				if(!(strcmp(inline_tags[i],cur_node->name)))
    				{
					flag=1;
					printf("[{<%s>}]", cur_node->name);
					break;
    				}
			}
			if(flag!=1)
			{
				printf("[<%s>]", cur_node->name);
			}
            		//printf("[{%s}]", cur_node->name);
        	}
        	else if(cur_node->type == XML_TEXT_NODE)
        	{
            		printf("%s", (char *)cur_node->content);
        	}
        	apert_format(cur_node->children);
    	}
}

int main(int argc, char **argv) 
{
	htmlDocPtr doc;
	xmlNode *roo_element = NULL;
    	if (argc != 2)  
    	{
        	printf("\nInvalid argument\n");
        	return(1);
    	}

    	
    	LIBXML_TEST_VERSION    

    	doc = htmlReadFile(argv[1], NULL, HTML_PARSE_NOBLANKS | HTML_PARSE_NOERROR | HTML_PARSE_NOWARNING | HTML_PARSE_NONET);
    	if (doc == NULL) 
    	{
        	fprintf(stderr, "Document not parsed successfully.\n");
        	return 0;
    	}

    	roo_element = xmlDocGetRootElement(doc);

    	if (roo_element == NULL) 
    	{
        	fprintf(stderr, "empty document\n");
        	xmlFreeDoc(doc);
        	return 0;
    	}
    	
	
	apert_format(roo_element);

    	xmlFreeDoc(doc);       // free document
    	xmlCleanupParser();    // Free globals
    	return 0;
}
