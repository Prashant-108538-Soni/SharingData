class _StickyDateHeader extends StatelessWidget {
  final String date;

  const _StickyDateHeader({required this.date});

  @override
  Widget build(BuildContext context) {
    return Container(
      color: Colors.transparent, // Keep transparent or use background if needed
      padding: const EdgeInsets.symmetric(vertical: 8),
      child: Align(
        alignment: Alignment.centerLeft,
        child: Container(
          margin: const EdgeInsets.only(left: 12),
          padding: const EdgeInsets.symmetric(horizontal: 12, vertical: 4),
          decoration: BoxDecoration(
            color: Colors.grey.shade200,
            borderRadius: BorderRadius.circular(20),
          ),
          child: Text(
            date,
            style: const TextStyle(
              fontWeight: FontWeight.w600,
              fontSize: 13,
              color: Colors.black87,
            ),
          ),
        ),
      ),
    );
  }
}