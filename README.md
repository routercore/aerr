# aerr

Shortcut for application errors.
In general every application internally needs to handler errors.

Following were found by us to be good practice:

- Do not try to use anything else except error interface.
- Internally in your appliation everything (not considering generic libraries) should be wrapped into aerr.
- Upper most layer such as HTTP endpoint handles error by translating error into http code and redering its content.
- You can easily clasify most errors int into few categories such as one outlined below.
- Try to be short descriptive, do not use capitalized sentences.
- Wrap your original errors.


## Code errors:

```golang
// CodeOK should be used as the codes.OK. Returned on success.
CodeOK 

// CodeCanceled indicates the operation was canceled (typically by the caller).
CodeCanceled 

// CodeUnknown error. An example of where this error may be returned is
// if an error value received from another address space belongs to
// an error-space that is not known in this address space. Also, errors
// raised by APIs that do not return enough error information
// may be converted to this error.
CodeUnknown 

// CodeInvalidArgument indicates client specified an invalid argument.
// Note that this differs from FailedPrecondition. It indicates arguments
// that are problematic regardless of the state of the system
// (e.g., a malformed file name, or validation errors).
CodeInvalidArgument 

// CodeDeadlineExceeded means operation expired before completion.
// For operations that change the state of the system, this error may be
// returned even if the operation has completed successfully. For
// example, a successful response from a server could have been delayed
// long enough for the deadline to expire.
CodeDeadlineExceeded 

// CodeNotFound means some requested entity or model (e.g., file or directory) was
// not found.
CodeNotFound 

// CodeAlreadyExists means an attempt to create an entity failed because one
// already exists.
CodeAlreadyExists 

// CodePermissionDenied indicates the caller does not have permission to
// execute the specified operation. It must not be used for rejections
// caused by exhausting some resource (use ResourceExhausted
// instead for those errors). It must not be
// used if the caller cannot be identified (use Unauthenticated
// instead for those errors).
CodePermissionDenied 

// CodeResourceExhausted indicates some resource has been exhausted, perhaps
// a per-user quota, or perhaps the entire file system is out of space.
//
// This error code will be generated by the gRPC framework in
// out-of-memory and server overload situations, or when a message is
// larger than the configured maximum size.
CodeResourceExhausted 

// CodeFailedPrecondition indicates operation was rejected because the
// system is not in a state required for the operation's execution.
// For example, directory to be deleted may be non-empty, a rmdir
// operation is applied to a non-directory, etc.
//
// A litmus test that may help a service implementor in deciding
// between CodeFailedPrecondition, CodeAborted, and CodeUnavailable:
//  (a) Use CodeUnavailable if the client can retry just the failing call.
//  (b) Use CodeAborted if the client should retry at a higher-level
//      (e.g., restarting a read-modify-write sequence).
//  (c) Use CodeFailedPrecondition if the client should not retry until
//      the system state has been explicitly fixed. E.g., if a "rmdir"
//      fails because the directory is non-empty, FailedPrecondition
//      should be returned since the client should not retry unless
//      they have first fixed up the directory by deleting files from it.
//  (d) Use CodeFailedPrecondition if the client performs conditional
//      REST Get/Update/Delete on a resource and the resource on the
//      server does not match the condition. E.g., conflicting
//      read-modify-write on the same resource.
CodeFailedPrecondition 

// CodeAborted indicates the operation was aborted, typically due to a
// concurrency issue like sequencer check failures, transaction aborts,
// etc.
//
// See litmus test above for deciding between CodeFailedPrecondition,
// CodeAborted, and CodeUnavailable.
CodeAborted 

// CodeOutOfRange means operation was attempted past the valid range.
// E.g., seeking or reading past end of file.
//
// Unlike CodeInvalidArgument, this error indicates a problem that may
// be fixed if the system state changes. For example, a 32-bit file
// system will generate CodeInvalidArgument if asked to read at an
// offset that is not in the range [0,2^32-1], but it will generate
// CodeOutOfRange if asked to read from an offset past the current
// file size.
//
// There is a fair bit of overlap between CodeFailedPrecondition and
// CodeOutOfRange. We recommend using CodeOutOfRange (the more specific
// error) when it applies so that callers who are iterating through
// a space can easily look for an CodeOutOfRange error to detect when
// they are done.
CodeOutOfRange 

// CodeUnimplemented indicates operation is not implemented or not
// supported/enabled in this service.
CodeUnimplemented 

// CodeInternal errors. Means some invariants expected by underlying
// system has been broken. If you see one of these errors,
// something is very broken.
CodeInternal 

// CodeUnavailable indicates the service is currently unavailable.
// This is a most likely a transient condition and may be corrected
// by retrying with a backoff. Note that it is not always safe to retry
// non-idempotent operations.
//
// See litmus test above for deciding between CodeFailedPrecondition,
// CodeAborted, and CodeUnavailable.
CodeUnavailable 

// CodeDataLoss indicates unrecoverable data loss or corruption.
CodeDataLoss 

// CodeUnauthenticated indicates the request does not have valid
// authentication credentials for the operation.
CodeUnauthenticated 
```


Credits:

- Jacek Kucharczyk
- Richard Hutta