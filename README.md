Row(
      crossAxisAlignment: CrossAxisAlignment.center,
      children: [
        // Icon with circular background
        Flexible(
          child: Container(
            padding: const EdgeInsets.all(8),
            decoration: BoxDecoration(shape: BoxShape.circle, color: backgroundColor),
            alignment: Alignment.center,
            child: SizedBox(
              width: 24,
              height: 24,
              child: SvgPicture.asset(
                svgPath,
                // Add placeholderBuilder for error handling
                placeholderBuilder: (BuildContext context) =>
                    const Icon(Icons.error_outline, color: Colors.red),
              ),
            ),
          ),
        ),
        Flexible(child: const SizedBox(width: 12)),
        Expanded(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              // Title text
              Flexible(
                child: Text(
                  eventName,
                  style: const TextStyle(fontWeight: FontWeight.w600, color: Colors.black87),
                  overflow: TextOverflow.ellipsis, // Optional: Add ellipsis for long event names
                  maxLines: 1, // Optional: Limit the event name to a single line
                ),
              ),
              const SizedBox(height: 4),
              // Account number | Bill Type
              Flexible(
                child: Row(
                  children: [
                    Expanded(
                      // Make the accountDetails Text widget flexible
                      child: Text(
                        accountDetails,
                        style: TextStyle(color: Colors.grey.shade800),
                        overflow: TextOverflow.ellipsis, // Add ellipsis for long account details
                        maxLines: 1, // Limit to a single line
                      ),
                    ),
                    const SizedBox(width: 6),
                    if (billType.isNotEmpty) Text('|', style: TextStyle(color: Colors.grey.shade800)),
                    const SizedBox(width: 6),
                    // Wrap billType with Expanded if it could also overflow
                    Expanded(
                      child: Text(
                        billType,
                        style: TextStyle(color: Colors.grey.shade800),
                        overflow: TextOverflow.ellipsis, // Add ellipsis for long bill types
                        maxLines: 1, // Limit to a single line
                      ),
                    ),
                  ],
                ),
              ),
            ],
          ),
        ),
      ],
    );
