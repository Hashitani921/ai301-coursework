# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s3`

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

I work mainly in Python on the backend: FastAPI services, Pydantic
models, SQLAlchemy, and pytest. I am comfortable reading a stack trace,
running a test suite, and tracing a request through a service layer, so a
bug with a reproduction and a named function is the kind of work I can
finish without a long ramp-up.

I also have working knowledge of AI and RAG systems, so retrieval,
chunking, embeddings, relevance scoring, and LLM output parsing are
familiar ground rather than unfamiliar vocabulary. Issues touching the
`rag`, `ingestion`, or `api` areas of this codebase are the ones I most
want, because the fix teaches me something I will reuse.

What I want to get better at is the contribution workflow itself: reading
someone else's codebase, reproducing a defect from an issue report, and
writing a change small enough to review. So I prefer an issue where the
expected behaviour is already stated and the failure is mechanical to
confirm, over one where I would have to design the feature first.

What I want to avoid on a first contribution: front-end and CSS work,
anything that needs a database migration or changes a public API
contract, and issues whose real difficulty is a product decision nobody
has made yet.
