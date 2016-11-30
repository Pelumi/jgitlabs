# jgitlabs
Experimenting with Jgit methods










            diff = diffStream.toString();
        } catch (IOException e) {
            Log.error("There was an exception closing stream", e);
        } finally {
            try {
                diffStream.close();
            } catch (IOException e) {
                Log.warn("There was an exception closing stream", e);
            }
        }

        return diff;
    }

    private AbstractTreeIterator prepareTreeParser(Repository repository, String ref) throws IOException {
        Ref head = repository.findRef(ref);
        RevWalk walk = new RevWalk(repository);
        RevCommit commit = walk.parseCommit(head.getObjectId());
        RevTree tree = walk.parseTree(commit.getTree().getId());

        CanonicalTreeParser oldTreeParser = new CanonicalTreeParser();
        ObjectReader oldReader = repository.newObjectReader();
        try {
            oldTreeParser.reset(oldReader, tree.getId());
        } finally {
            oldReader.close();
        }
        return oldTreeParser;
    }

}

